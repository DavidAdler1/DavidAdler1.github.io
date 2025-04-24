# Diagrams

This page contains all the project diagrams, organized by type. These diagrams illustrate the architecture, relationships, and workflows within David's Grand Shop.

---
<details>
<summary>Controller Diagrams</summary>

![LoginController UML](Images/UML%20Diagrams/LoginControllerUML.png)  
*LoginController - Manages user authentication, session creation, and login success/failure handling*  

![ProductsController UML](Images/UML%20Diagrams/ProductsControllerUML.png)  
*ProductsController - Handles product browsing and search for authenticated users only*  

![RegistrationController UML](Images/UML%20Diagrams/RegistrationControllerUML.png)  
*RegistrationController- Handles new user registration with validation and admin flag initialization*  

![CartController UML](Images/UML%20Diagrams/CCUML.png)  
*CartController - Manages cart operations: add, remove, clear items, and checkout process validation*  

![AdminController UML](Images/UML%20Diagrams/ACUML.png)  
*AdminController - Provides admin-only product CRUD and user management with session checks*  

![ProfileController UML](Images/UML%20Diagrams/PCUML.png)  
*ProfileController - Manages logged-in user profile viewing and editing functionality*  

![OrderController UML](Images/UML%20Diagrams/OCUML.png)  
*OrderController - Processes checkout, creates orders, updates inventory, and displays order history*  

</details>

---

<details>
<summary>Model Diagrams</summary>

![RegistrationModel UML](Images/UML%20Diagrams/RegistrationModelUML.png)  
*RegistrationModel - Contains user registration data, including personal details and admin status*  

![CartItemModel UML](Images/UML%20Diagrams/CIMUML.png)  
*CartItemModel - Represents shopping cart items with product info and quantity*  

![UserModel UML](Images/UML%20Diagrams/UMUML.png)  
*UserModel - Basic user authentication model with username, password hash, and admin flag*  

![ProductModel UML](Images/UML%20Diagrams/PMUML.png)  
*ProductModel - Stores product details including name, price, description, and inventory quantity*  

![OrderModel UML](Images/UML%20Diagrams/OMUML.png)  
*OrderModel - Represents completed orders with user info, date, and list of items*  
</details>

---

<details>
<summary>Service & DAO Diagrams</summary>

![OrderService UML](Images/UML%20Diagrams/OSUML.png)  
*OrderService - Creates orders with transaction handling, inventory updates, and retrieves order history directly from the database*    

![ProductDataService UML](Images/UML%20Diagrams/IProductDataServiceUML.png)  
*IProductDataService- Interface defining standard product data operations*  

![ProductDAO UML](Images/UML%20Diagrams/PDAOUML.png)  
*ProductDAO- Implements product CRUD operations and search functionality using SQL commands*  

![SecurityService UML](Images/UML%20Diagrams/SSUML.png)  
*SecurityService - Provides user authentication, registration, and CRUD operations through SecurityDAO*  

![SecurityDAO UML](Images/UML%20Diagrams/SDAOUML.png)  
*SecurityDAO - Handles database operations for user authentication, registration, and profile management* 

![CartService UML](Images/UML%20Diagrams/CSUML.png)  
*CartService - Manages cart operations using cookie-based persistence with JSON serialization*  

</details>

---

<details>
<summary>User Experience Diagrams</summary>

![User View Diagram](Images/View%20Diagrams/UserDiagram.png)  
*User View - Shows customer journey from login to browsing, viewing their profile, cart management, and checkout*  

![Admin View Diagram](Images/View%20Diagrams/AdminViewDiagram.png)  
*Admin View - Illustrates admin-specific interface for product and user management* 

</details>

---

<details>
<summary>Architecture Diagram</summary>

![Architecture Diagram](Images/Architecture%20Diagram/Architecture%20Diagram.png)   
*Architecture Diagram - MVC pattern with controller, service, and DAO layers connected to SQL Server* 

</details>


---

<details>
<summary>ER Diagram</summary>

![ER Diagram](Images/ER%20Diagram/ER%20Diagram.png)  
*ER Diagram - Database schema showing relationships between Users, Products, Orders, and OrderItems tables* 

</details>
