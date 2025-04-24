# Diagrams

This page contains all the project diagrams, organized by type. These diagrams illustrate the architecture, relationships, and workflows within David's Grand Shop.

---

## Controller Diagrams

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



---


## Model Diagrams

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


---


## Service & DAO Diagrams

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



---


## User Experience Diagrams

![User View Diagram](Images/View%20Diagrams/UserDiagram.png)  
*User View - Shows customer journey from login to browsing, viewing their profile, cart management, and checkout*  

![Admin View Diagram](Images/View%20Diagrams/AdminViewDiagram.png)  
*Admin View - Illustrates admin-specific interface for product and user management* 


---

## Flow Diagram

![Order History Flow](Images/Flow%20Diagrams/OrderHistory.png)  
*Order History Flow - Describes the steps involved in retrieving and displaying past orders for a user*

![Products Flow](Images/Flow%20Diagrams/Products.png)  
*Products Flow - Shows the process of loading, filtering, and displaying products to users*

![Products Page Flow](Images/Flow%20Diagrams/ProductsPage.png)  
*Products Page Flow - Illustrates UI interactions and logic behind the products listing page*

![Registration Flow](Images/Flow%20Diagrams/Registration.png)  
*Registration Flow - Depicts the user registration sequence with validation and database interaction*

![User Profile Flow](Images/Flow%20Diagrams/UserProfile.png)  
*User Profile Flow - Displays the process of viewing and editing user profile data*

![Admin Product Flow](Images/Flow%20Diagrams/AdminProduct.png)  
*Admin Product Flow - Describes the admin's product management steps, including edit and delete*

![Admin User Flow](Images/Flow%20Diagrams/AdminUser.png)  
*Admin User Flow - Outlines user management functionalities available to admins*

![Cart Flow](Images/Flow%20Diagrams/Cart.png)  
*Cart Flow - Shows how cart items are added, stored, and retrieved during a session*

![Cart Management Flow](Images/Flow%20Diagrams/CartManagement.png)  
*Cart Management Flow - Details user interactions for modifying and clearing the cart*

![Checkout Flow](Images/Flow%20Diagrams/Checkout.png)  
*Checkout Flow - Highlights the process of validating, confirming, and storing an order*


## Architecture Diagram

![Architecture Diagram](Images/Architecture%20Diagram/Architecture%20Diagram.png)   
*Architecture Diagram - MVC pattern with controller, service, and DAO layers connected to SQL Server* 




---


## ER Diagram

![ER Diagram](Images/ER%20Diagram/ER%20Diagram.png)  
*ER Diagram - Database schema showing relationships between Users, Products, Orders, and OrderItems tables* 



---
## Project Navigation

[Home](README.md)

[Application Demo](Demo.md)

[Project Approach](Approach.md)

[Setup & Installation Guide](Setup.md)

[Key Code Snippets & Implementation](Code_Snippets.md)

