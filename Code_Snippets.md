# Code Snippets, Key Implementation Logic

This document highlights important code patterns and implementation techniques used in Davids Grand Shop. Each section demonstrates best practices in modern web development and explains why these approaches matter.

---

Controller Layer: AdminController

<details>

     public class AdminController : Controller
    {
    private readonly IHttpContextAccessor _context;
    private readonly ProductDAO repository;
    private readonly SecurityService _securityService;

    public AdminController(IHttpContextAccessor context, SecurityService securityService, IConfiguration configuration)
    {
        _context = context;
        _securityService = securityService;
        repository = new ProductDAO(configuration);
    }

    //helper method to check if the user is an admin
    private bool IsAdminUser()
    {
    string userName = _context.HttpContext.Session.GetString("UserName");
    bool IsAdmin = _context.HttpContext.Session.GetInt32("IsAdmin") == 1;
    return !string.IsNullOrEmpty(userName) && IsAdmin;
    }

    //admin can delete products
    public IActionResult DeleteProduct(int id)
    {
    if (!IsAdminUser())
    {
        return RedirectToAction("Index", "Home");
    }

    repository.Delete(id);
    return View("Product/Index", repository.AllProducts());
    }
    }
    
The AdminController is designed with security in mind, checking user roles for each action. It uses dependency injection to keep components loosely connected and delegates data tasks to the right services.

</details>

---

Service Layer: CartService

<details>

    public class CartService
    {
    private readonly IHttpContextAccessor _contextAccessor;
    private const string CartCookieKey = "TheCart";
    
    ///retrieves the current shopping cart from cookies.
    /// </summary>
    /// <returns>The list of items in the shopping cart.</returns>
    public List<CartItemModel> GetCart()
    {
    var cookies = _contextAccessor.HttpContext.Request.Cookies[CartCookieKey];
    if (string.IsNullOrEmpty(cookies))
    {
        return new List<CartItemModel>();
    }

    return JsonSerializer.Deserialize<List<CartItemModel>>(cookies);
    }

    ///saves the current shopping cart to cookies with a lifespan of 6 months.
    /// </summary>
    /// <param name="cart">The shopping cart to save.</param>
    public void SaveCart(List<CartItemModel> cart)
    {
    var cartJson = JsonSerializer.Serialize(cart);
    var options = new CookieOptions
    {
        Expires = DateTime.Now.AddMonths(6),
        HttpOnly = true,
        Secure = true,
        SameSite = SameSiteMode.Lax
    };

    _contextAccessor.HttpContext.Response.Cookies.Append(CartCookieKey, cartJson, options);
    }

    ///adds a product and its quantity to the shopping cart.
    /// </summary>
    /// <param name="product">the product to add.</param>
    /// <param name="quantity">the quantity of the product to add.</param>
    public void AddToCart(ProductModel product, int quantity)
    {
    var cart = GetCart();
    var existingItem = cart.FirstOrDefault(i => i.ProductId == product.Id);

    if (existingItem != null)
    {
        existingItem.Quantity += quantity;
    }
    else
    {
        cart.Add(new CartItemModel(product.Id, product.Name, product.Price, quantity));
    }

    SaveCart(cart);
    }
    
CartService is built without storing user state on the server. It securely uses cookies (with HttpOnly, Secure, and SameSite flags) to keep data safe, and offers a simple interface that hides how the data is stored.
  
</details>

---

DAO Usage: ProductDAO

<details>

    public class ProductDAO : IProductDataService
    {
    public List<ProductModel> AllProducts()
    {

    //assume nothing is found
    List<ProductModel> foundProducts = new List<ProductModel>();

    //uses prepared statements for security, username and password are defined below

    string sqlStatement = "SELECT * FROM dbo.Product";

    using (SqlConnection connection = new SqlConnection(connectionString))
    {
        SqlCommand command = new SqlCommand(sqlStatement, connection);


        try
        {
            connection.Open();
            SqlDataReader reader = command.ExecuteReader();

            while (reader.Read())
            {
				foundProducts.Add(new ProductModel(
					(int)reader["Id"],
					(string)reader["Name"],
					(decimal)reader["Price"],
					(string)reader["Description"],
					(int)reader["Quantity"])
                                                );
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
    return foundProducts;
    }

    public List<ProductModel> SearchProducts(string searchTerm)
    {
      
      //assume nothing is found
      List<ProductModel> foundProducts = new List<ProductModel>();

    //uses prepared statements for security, username and password are defined below
    string sqlStatement = "SELECT * FROM dbo.Product WHERE Name LIKE @name";

    using (SqlConnection connection = new SqlConnection(connectionString))
    {
        SqlCommand command = new SqlCommand(sqlStatement, connection);

        //define the values of the two placeholders in the sql statement string
        command.Parameters.AddWithValue("@name", '%' + searchTerm + '%');


        try
        {
            connection.Open();
            SqlDataReader reader = command.ExecuteReader();

            while (reader.Read())
			{
				foundProducts.Add(new ProductModel(
					(int)reader["Id"],
					(string)reader["Name"],
					(decimal)reader["Price"],
					(string)reader["Description"],
					(int)reader["Quantity"]));
			}
		}
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
    return foundProducts;
    }

ProductDAO follows the Repository pattern to organize data access. It uses parameterized queries to prevent SQL injection, handles resources safely with using statements, and includes error handling to keep the app stable

</details>

---

Transaction Handling: OrderService

<details>

    public class OrderService
    {
    
    private readonly string connectionString;

    public bool CreateOrder(OrderModel order)
    {
        bool success = false;

        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            connection.Open();
            // Begin a transaction to ensure atomicity
            using (SqlTransaction transaction = connection.BeginTransaction())
            {
                try
                {
                    // insert the order
                    string insertOrderSql = "INSERT INTO Orders (UserName, OrderDate) OUTPUT INSERTED.Id VALUES (@UserName, @OrderDate)";
                    using (SqlCommand orderCmd = new SqlCommand(insertOrderSql, connection, transaction))
                    {
                        orderCmd.Parameters.AddWithValue("@UserName", order.UserName);
                        orderCmd.Parameters.AddWithValue("@OrderDate", order.OrderDate);
                        order.Id = (int)orderCmd.ExecuteScalar();
                    }

                    foreach (var item in order.Items)
                    {
                        // check inventory
                        string checkInventorySql = "SELECT Quantity FROM Product WHERE Id = @ProductId";
                        int availableQuantity = 0;
                        using (SqlCommand checkCmd = new SqlCommand(checkInventorySql, connection, transaction))
                        {
                            checkCmd.Parameters.AddWithValue("@ProductId", item.ProductId);
                            var result = checkCmd.ExecuteScalar();
                            if (result != null)
                                availableQuantity = Convert.ToInt32(result);
                            else
                                throw new Exception($"Product with Id {item.ProductId} not found.");
                        }

                        // validate inventory
                        if (item.Quantity > availableQuantity)
                            throw new Exception($"Insufficient inventory for product '{item.ProductName}'");

                        // insert order item & update inventory
                    }

                    //commit the transaction if all operations succeed
                    transaction.Commit();
                    success = true;
                }
                catch (Exception ex)
                {
                    //roll back all operations if any error occurs
                    transaction.Rollback();
                    Console.WriteLine($"Error in CreateOrder: {ex.Message}");
                }
            }
        }
        return success;
    }
    }
    
OrderService uses reliable transactions that follow ACID principles to keep data consistent. If something goes wrong during order creation or inventory updates, it rolls back the changes to prevent errors and maintain stability.

</details>

---

Security Implementation: SecurityDAO
 
<details>

    public class SecurityDAO
    {
    //connection string for the database
    private readonly string connectionString;

    ///authenticates a user by verifying their username and password hash.
      /// </summary>
    /// <param name="user">user model with username and password</param>
    /// <returns>true if user exists, otherwise false</returns>
    public bool FindUserByNameAndPassword(UserModel user)
    {
    bool isSuccessful = false; 

    string sqlStatement = "SELECT * FROM [RegistrationMain] WHERE UserName = @userName AND PasswordHash = @password";

    using (SqlConnection connection = new SqlConnection(connectionString))
    {
        SqlCommand command = new SqlCommand(sqlStatement, connection);
        command.Parameters.AddWithValue("@userName", user.UserName);
        command.Parameters.AddWithValue("@password", user.PasswordHash);

        try
        {
            connection.Open();
            SqlDataReader reader = command.ExecuteReader();

            if (reader.HasRows)
            {
                reader.Read();
                //retrieve user id
                user.Id = reader.GetInt32(reader.GetOrdinal("Id")); 
                //retrieve if is admin
                user.IsAdmin = reader.GetBoolean(reader.GetOrdinal("IsAdmin")); 
                isSuccessful = true;
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error in FindUserByNameAndPassword: {ex.Message}");
        }
    }

    return isSuccessful;
    }

    ///registers a new user
    /// </summary>
    /// <param name="user">user registration model</param>
    /// <returns>true if registration is successful, otherwise false</returns>
    public bool RegisterUser(RegistrationModel user)
    {
    bool isSuccess = false;

    string sqlStatement = @"
    INSERT INTO [RegistrationMain] (FirstName, LastName, Sex, Age, State, Email, Username, PasswordHash, IsAdmin)
    VALUES (@FirstName, @LastName, @Sex, @Age, @State, @Email, @Username, @PasswordHash, @IsAdmin)";

    using (SqlConnection connection = new SqlConnection(connectionString))
    {
        SqlCommand command = new SqlCommand(sqlStatement, connection);

        // Set parameter values, handling null cases
        command.Parameters.AddWithValue("@FirstName", user.FirstName);
        command.Parameters.AddWithValue("@LastName", user.LastName);
        command.Parameters.AddWithValue("@Sex", user.Sex ?? (object)DBNull.Value);
        command.Parameters.AddWithValue("@Age", user.Age.HasValue ? (object)user.Age : DBNull.Value);
        command.Parameters.AddWithValue("@State", user.State ?? (object)DBNull.Value);
        command.Parameters.AddWithValue("@Email", user.Email);
        command.Parameters.AddWithValue("@Username", user.Username);
        command.Parameters.AddWithValue("@PasswordHash", user.Password);
        command.Parameters.AddWithValue("@IsAdmin", user.IsAdmin);

        try
        {
            connection.Open();
            int rowsAffected = command.ExecuteNonQuery();
            isSuccess = rowsAffected == 1; // Ensure exactly one row was inserted
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error in RegisterUser: {ex.Message}");
        }
    }

    return isSuccess;
    }
    
SecurityDAO handles authentication securely by using parameterized queries to block SQL injection. It also checks for null values to prevent database errors and validates input to keep data accurate and safe.

</details>

---

Model Validation: Data Annotations

<details>

    public class RegistrationModel
    
    {
      
    [Key]
    public int Id { get; set; }

    [Required]
    [DisplayName("First Name")]
    public string FirstName { get; set; }

    [Required]
    [DisplayName("Last Name")]
    public string LastName { get; set; }

    [Required]
    [DisplayName("Sex")]
    public string Sex { get; set; }

    [Required]
    [DisplayName("Age")]
    public int? Age { get; set; }

    [Required]
    [DisplayName("State")]
    public string State { get; set; }

    [Required]
    [DisplayName("Email")]
    public string Email { get; set; }

    [Required]
    [DisplayName("Username")]
    public string Username { get; set; }

    [Required]
    [DisplayName("Password")]
    public string Password { get; set; }

    public bool IsAdmin { get; set; }
    }


    public class ProductModel
    {
    
    public int Id { get; set; }
    
    public string? Name { get; set; }
    
    public decimal Price { get; set; }
    
    public string? Description { get; set; }
    
    [DisplayName("Quantity in Stock")]
    public int Quantity { get; set; }
    
    // Parameterized constructor for model initialization
    public ProductModel(int id, string? name, decimal price, string? description, int quantity)
    {
        Id = id;
        Name = name;
        Price = price;
        Description = description;
        Quantity = quantity;
    }
    
    // Default constructor
    public ProductModel() { }
    }

ProductModel uses data annotations to enforce validation rules and customize how data is shown. It supports nullable reference types for better safety and uses constructors to properly set up objects and support immutability.

</details>

## Project Navigation

[Home](README.md)

[Application Demo](Demo.md)

[Project Approach](Approach.md)

[Setup & Installation Guide](Setup.md)

[Project Diagrams & Architecture](diagrams.md)

---


