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
