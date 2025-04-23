# Setup Guide

This guide explains how to set up and run David's Grand Shop locally.

---

Prerequisites

Visual Studio 2022
SQL Server (LocalDB or Express)
.NET 6.0 SDK

---

## Installation Steps

### Clone the repository:

- git clone https://github.com/DavidAdler1/DavidsGrandShop.git

### Open the solution in Visual Studio 2022
- Update the connection string in appsettings.json to match your SQL Server:

json"ConnectionStrings": {
  "DefaultConnection": "Server=(localdb)\\MSSQLLocalDB;Database=Capstone;Trusted_Connection=True;MultipleActiveResultSets=true"
}

--- 
Database Setup
<details>

1. Create a new database named Capstone in SQL Server
   
2. Execute the following SQL scripts to create the required tables:

SQL
CREATE TABLE Orders (
    Id INT PRIMARY KEY IDENTITY,
    UserName NVARCHAR(100) NOT NULL,
    OrderDate DATETIME NOT NULL
);

CREATE TABLE OrderItems (
    Id INT PRIMARY KEY IDENTITY,
    OrderId INT FOREIGN KEY REFERENCES Orders(Id),
    ProductId INT NOT NULL,
    Quantity INT NOT NULL,
    Price DECIMAL(18, 2) NOT NULL
);

CREATE TABLE [dbo].[Product] (
    [Id]          INT             NOT NULL,
    [Name]        NVARCHAR (50)   NULL,
    [Price]       DECIMAL (18, 2) NULL,
    [Description] NVARCHAR (500)  NULL,
    [Quantity]    INT             DEFAULT ((0)) NOT NULL,
    PRIMARY KEY CLUSTERED ([Id] ASC)
);

CREATE TABLE [dbo].[RegistrationMain] (
    [Id]           INT            IDENTITY (1, 1) NOT NULL,
    [FirstName]    NVARCHAR (50)  NOT NULL,
    [LastName]     NVARCHAR (50)  NOT NULL,
    [Sex]          NVARCHAR (10)  NULL,
    [Age]          INT            NULL,
    [State]        NVARCHAR (50)  NULL,
    [Email]        NVARCHAR (255) NOT NULL,
    [Username]     NVARCHAR (50)  NOT NULL,
    [PasswordHash] NVARCHAR (255) NOT NULL,
    [isAdmin]      BIT            DEFAULT ((0)) NULL,
    PRIMARY KEY CLUSTERED ([Id] ASC),
    UNIQUE NONCLUSTERED ([Username] ASC)
);

3. Add sample users for testing:
   -- Insert admin user
INSERT INTO [dbo].[RegistrationMain] ([FirstName], [LastName], [Sex], [Age], [State], [Email], [Username], [PasswordHash], [isAdmin])
VALUES ('Admin', 'User', 'Male', 25, 'Arizona', 'davidadler28@gmail.com', 'Jack', 'Skellington', 1);

-- Insert regular user
INSERT INTO [dbo].[RegistrationMain] ([FirstName], [LastName], [Sex], [Age], [State], [Email], [Username], [PasswordHash], [isAdmin])
VALUES ('Regular', 'User', 'Female', 25, 'California', 'Jackie@AoL.com', 'Jackie', 'CoolMom', 0);

</details>

---

### Build the solution (press Ctrl+Shift+B)
### Run the application (press F5)

### Test Accounts

Admin User: username = Jack, password = Skellington
Regular User: username = Jackie, password = CoolMom

### Live Access
You can also access the deployed version of this application at:
[https://github.com/DavidAdler1/DavidsGrandShop](https://capstoneproject20250422140909-fxf3hfdrcrg5eshr.canadacentral-01.azurewebsites.net/)
