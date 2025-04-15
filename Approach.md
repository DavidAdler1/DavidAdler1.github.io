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
- Connected to SQL Server using ADO.NET and SqlConnection.
- Protected all data access with parameterized queries to prevent SQL injection.

### Frontend

- Built with HTML, CSS, and Razor.
- Implemented clean and responsive views.
- Used TempData to handle success and error messages between requests.
- Used cookies to persist cart data between sessions.

---

## Authentication & Session Management

- Utilized IHttpContextAccessor to manage and access session data across the application.
- Tracked user login status, username, and admin privileges using session variables.
- Implemented secure cart persistence by storing cart data in cookies with HttpOnly, Secure, and SameSite attributes

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

Deployment
- The application was deployed to the cloud using AWS, making it accessible for demonstration and testing by others.

---

## Testing Tools

Jira
- Used to track bugs and issues throughout the development process. Each sprint included a dedicated testing phase to verify functionality against user stories and test cases.

GitHub
- Version control was managed with GitHub, allowing testing of changes through pull requests and branches.

Postman
- Used to manually test backend logic and API responses. Helped ensure requests and responses were functioning correctly.
