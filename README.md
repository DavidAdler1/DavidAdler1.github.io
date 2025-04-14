# Davids Grand Shop - Capstone Project Portfolio


### High-level Functional Requirements

User Registration & Login

- Users can create an account and log in securely.

- Session-based authentication ensures only logged-in users can access the website

Product Browsing & Search

- Users can view all products and search by name or keyword.

Shopping Cart Functionality

- Users can add, remove, and update products in their cart.

- Cart data persists between sessions using cookies.

Checkout & Order Processing

- Logged-in users can place an order.

- Product inventory is updated in the database after checkout.

Order History & User Profiles

- Users can view their order history and update personal information.

Admin Controls

- Admin users can view, edit, or delete products.

- Admins can view, edit, or delete the list of all registered users.

### High Level Non-Functional Requirements
Security

- Uses secure sessions for authentication.

- Admin access protected by isAdmin flag.

- Data validation and SQL injection protection via parameterized queries.

Performance

- Lightweight ADO.NET access means fast, direct SQL communication.

- Optimized queries minimize server load and improve responsiveness.

Scalability

- Clean MVC architecture with service layers allows easy scaling of features.

- Modular codebase allows new services and views to be added independently.

Maintainability

- Follows good principles with the separation of concerns between controllers, services, models, and views.

- Business logic is encapsulated in services, making the system easy to update or debug.

Usability

- Clean and easy-to-use user interface for both customers and admins.

Reliability

- SQL transactions prevent data inconsistency during checkout.

- ILogger helps detect and resolve issues fast.

### Technologies Chosen

- ASP.NET MVC (C#) – For its clear structure and separation of concerns using the Model-View-Controller pattern. It made my app more organized and maintainable.

- SQL Server – To store all user, product, and order data. It’s secure, reliable, and works well with .NET.

- ADO.NET – For direct communication with the database using SQL queries. It gave me full control over how I handled data.

- HTML, CSS, and Razor – For building clean and dynamic views. Razor let me combine C# and HTML easily for interactive pages.

- IHttpContextAccessor – For managing user sessions like login state, admin roles, and the shopping cart. I chose this to be able to use user data.

- ILogger – For tracking user activity, especially logins, and handling any errors for debugging.

### Industry Best Practices
- Separation of Concerns – I followed the MVC architecture to separate the user interface, business logic, and data access, making the code easier to manage and scale.

- Security Practices – I used session-based authentication and added user roles to control access to admin features.

- Service Layer Architecture – I created service classes like CartService, OrderService, and SecurityService to handle business logic separately from the controllers.

- Input Validation and Error Handling – I added checks during checkout, such as filtering out products with zero quantity, and used TempData for user-friendly error messages.

- Code Reusability and Modularity – Reusable methods and structured models made it easier to maintain and extend the project later.

- Secure Cookie Handling – I used HttpOnly, Secure, and SameSite cookie options when saving cart data to prevent tampering and cross-site attacks.
  
### Cloud Deployment
- Yes, my project is deployed to the cloud using AWS.
  
### How were DevOps principles applied?
This Project Followed the full Software Development Life Cycle.​

- Jira was used for sprint planning and management.​

- GitHub was used for code updates and version control.​

- Postman was used for API Testing and development.
  
### New Technologies Learned
- Learned about MVC architecture to better organize the project.

- Learned Jira for sprint planning and task tracking.

- Improved skills with Postman for API testing.

- Gained experience with GitHub for version control and collaboration.

- Learned session handling to manage user authentication and state.

### Technical Approach
Followed the MVC (Model-View-Controller) design pattern to separate concerns:

- Models for data representation

- Views for the UI

- Controllers for user interaction and routing

- Used Service Classes to handle business logic like cart operations and order processing.

- Implemented Session and Cookie Handling for user authentication and cart persistence.

- Used SQL Server for database storage and interaction via ADO.NET with SqlConnection.

- Applied Form Validation and input sanitization to ensure secure and clean data handling.

  
### Diagrams
For a detailed view of all the diagrams, please visit the [Diagrams Page](diagrams.md).


### Risks and Challenges
- Challenge: Integrating the frontend with the backend and ensuring smooth data flow.
- Solution: Used the MVC pattern to separate concerns and tested functionality frequently.

- Challenge: Managing user sessions and cart persistence, ensuring the cart remains intact even after page refreshes.
- Solution: Implemented cookie-based cart management using the CartService and session handling for user authentication.

- Challenge: Managing time constraints while interacting with issues that persist as development continues.
- Solution: Prioritized simple features first. Debugged issues as they came up.
  
- Challenge: Managing time constraints while addressing issues that persisted as development continued.
- Solution: Prioritized simpler features first and debugged issues as they came up to avoid delaying progress.

Resources Used: 
- ASP.NET MVC documentation, Stack Overflow, and  GCU Course C#3, Jira, GitHub, Postman.
- https://stackoverflow.com/questions/39860045/how-do-i-use-cookies-to-store-shopping-cart-content
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference
-  https://stackoverflow.com/questions/72875803/asp-net-core-identity-check-isadmin
  


### Outstanding Issues
- No outstanding issues with the project.

