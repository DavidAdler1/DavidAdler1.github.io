# Project Approach

This document outlines the approach taken to plan, design, and implement the Capstone Project. It includes design philosophy, architecture decisions, development methodology, and lessons learned.

---

## Architectural Approach

The project followed the **Model-View-Controller (MVC)** architecture:

- Models represent the data.
- Views present the data to users using Razor pages.
- Controllers manage logic and user interaction.

## Service Classes

To separate business logic from controllers, custom service classes were created:

- CartService – handles cart operations like adding, updating, and clearing items.
- OrderService – processes orders, updates inventory, and stores order history.
- SecurityService – manages user authentication, session validation, and admin access.
- SecurityDAO – connects to the database to validate login credentials securely.
- ProductDAO – manages product data, including fetching, updating, and deleting products.
- IProductDataService – interface to abstract product data operations for flexibility and testability.

---

## Implementation Strategy

### Backend
- Built using ASP.NET MVC with C#.

- Connected to SQL Server using ADO.NET and SqlConnection for direct database communication.

- Data access is secured through parameterized queries to prevent SQL injection vulnerabilities.

For a detailed list of technologies used, refer to the Technologies Chosen section in the README.

### Frontend
- Developed using HTML, CSS, and Razor to create dynamic, responsive views.

- Utilized TempData to manage success and error messages between requests.

- Implemented cookie-based persistence for cart data, ensuring the cart remains intact between sessions.

For more information on frontend technologies, check the Technologies Chosen section in the README.

---

## Authentication & Session Management

- Managed session data using IHttpContextAccessor, ensuring consistent access to session information across the application.

- Tracked user login status, username, and admin privileges using session variables for secure and efficient session management.

- Ensured secure cart persistence by storing cart data in cookies with HttpOnly, Secure, and SameSite attributes to prevent tampering and mitigate cross-site attacks.

For more details on security practices and session handling, refer to the Security section in the README.

---

## Development Process

For the development of this project, I followed a structured Software Development Life Cycle (SDLC) approach:

Analysis
- Requirements were gathered and broken down into user stories, identifying both functional and non-functional needs. This included login features, cart handling, admin roles, and product inventory control.

Design
- System architecture was planned using the MVC pattern. Diagrams such as ERD and use case diagrams were created to visualize database relationships and user interactions.

Development
- Core features were implemented using ASP.NET MVC, C#, and SQL Server. Business logic was separated into service classes for maintainability, and Razor was used to create dynamic views.

Testing
- Manual testing and debugging were performed regularly during sprints. Test cases were used to validate user registration, login, cart operations, and admin privileges. Tools like Postman were also used to simulate API interactions.

---

## Project Reflection

### What I Learned

Technical Skills:
- MVC Architecture – Learned how separating parts of the app into Models, Views, and Controllers makes the code easier to manage and test.

- Service Layer Design – Figured out how to keep business logic out of controllers for cleaner, more organized code.

- Security – Gained experience adding login protection, user roles, and secure data handling.

- Transaction Management – Learned how to safely manage database changes, especially when handling orders and inventory.

- Cookie Management – Used secure cookies to store cart data without relying on server-side sessions.

Professional Growth:
- Planning – Got better at breaking down features and estimating how long things will take.

- Problem-Solving – Improved how I debug and tackle tricky technical issues.

- Documentation – Learned to write clearer comments and explain design choices in my code.

- Time Management – Practiced prioritizing tasks and staying on schedule.

What Went Well
- Clean Architecture – Using MVC and service layers kept the project structured and easy to update.

- Security – Building security from the start helped avoid major issues later.

- Cart Persistence – The cookie-based cart system worked reliably and remembered items between sessions.

- Database Access – Using parameterized queries with ADO.NET kept things fast and secure.

- Role-Based Access – Splitting admin and user access helped control who could do what in the app.

What I’d Do Differently
- Test-Driven Development – I would write automated tests earlier to catch bugs sooner.

- Research - I would do more research on industry best practices to implement for security reasons.

- Design – I’d focus more on researching the topic, and what I could do to stand out as an E-commerce website

- Logging – I’d set up logging earlier to help with debugging and tracking issues.

- Code Reviews – I’d ask for more feedback from others to improve the code and design.


Future Enhancements
- Payment Integration – Add a way for users to pay for their orders securely.

- Email Confirmation – Have the order confirmation send an email to the user after placing an order.

- Better Search – Improve the search feature with filters and sorting options.

- Improve UI – Improve login and registration to be more restricted.

- Automated Testing – Add more tests to keep the app stable during future updates.

This project gave me valuable experience in full-stack web development using ASP.NET MVC. It reinforced how important good architecture is for building apps that are easy to maintain and secure. Working through challenges like session handling and database transactions helped me grow as a developer and will help in future projects.

## Project Navigation

[Home Page](README.md)

[Application Demo](Demo.md)

[Setup & Installation Guide](Setup.md)

[Key Code Snippets & Implementation](Code_Snippets.md)

[Project Diagrams & Architecture](diagrams.md)

