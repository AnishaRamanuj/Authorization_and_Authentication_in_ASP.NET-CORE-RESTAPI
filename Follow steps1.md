# THIS ARE THE STEPS FOR THE AUTHENTICATION PROCESS FROM SCRATCH

# Introduction
In this article, we are going to create a web application using .Net 6.0 and ASP.Net Core and also implement JWT Authentication.

JWT stands for JSON Web Token digitally signed using a secret key by a token provider. It helps the resource server to verify the token data using the same secret key.

JWT consists of three parts:

Header: encoded data of the token type and the algorithm used to sign the data.
Payload: encoded data of claims intended to share.
Signature: created by signing (encoded header + encoded payload) using a secret key.
Here I am going to use Visual Studio 2022 and SQL Server 2014.

# STEP-1 : Creating Tables

### First, we will create a database named “JWTAuthentication” or we can use any name and create two tables “UserInfo” and “Employee”. Open SQL Server and paste the below query to create the tables.
```RUBY
USE [JWTAuthentication]

CREATE TABLE [dbo].[UserInfo](
	[UserId] [int] IDENTITY(1,1) NOT NULL,
	[DisplayName] [varchar](60) NOT NULL,
	[UserName] [varchar](30) NOT NULL,
	[Email] [varchar](50) NOT NULL,
	[Password] [varchar](20) NOT NULL,
	[CreatedDate] [datetime] NOT NULL,
	CONSTRAINT [PK_UserInfo] PRIMARY KEY CLUSTERED
	(
		[UserId] ASC
	)
)
INSERT [dbo].[UserInfo] VALUES (N'Anisha ', N'Admin', N'admin@abc.com', N'$admin@2022', CAST(N'2022-01-17 14:47:58.207' AS DateTime))
```
```RUBY
CREATE TABLE [dbo].[Employee](
	[EmployeeID] [int] NOT NULL,
	[NationalIDNumber] [nvarchar](15) NOT NULL,
	[EmployeeName] [nvarchar](100) NULL,
	[LoginID] [nvarchar](256) NOT NULL,
	[JobTitle] [nvarchar](50) NOT NULL,
	[BirthDate] [date] NOT NULL,
	[MaritalStatus] [nchar](1) NOT NULL,
	[Gender] [nchar](1) NOT NULL,
	[HireDate] [date] NOT NULL,
	[VacationHours] [smallint] NOT NULL,
	[SickLeaveHours] [smallint] NOT NULL,
	[rowguid] [uniqueidentifier] ROWGUIDCOL  NOT NULL,
	[ModifiedDate] [datetime] NOT NULL,
	CONSTRAINT [PK_Employee] PRIMARY KEY CLUSTERED
	(
		[EmployeeID] ASC
	)
)
INSERT [dbo].[Employee] VALUES (1, N'295847284', N'Anisha Ramanuj', N'adventure-works\ken0', N'Developer', CAST(N'2001-05-22' AS Date), N'S', N'F', CAST(N'2022-01-14' AS Date), 99, 69, N'f01251e5-96a3-448d-981e-0f99d789110d', CAST(N'2022-06-30 00:00:00.000' AS DateTime))
INSERT [dbo].[Employee] VALUES (2, N'245797967', N'Anchal Shukla', N'adventure-works\terri0', N'Developer', CAST(N'2000-08-01' AS Date), N'S', N'F', CAST(N'2022-01-31' AS Date), 1, 20, N'45e8f437-670d-4409-93cb-f9424a40d6ee', CAST(N'2022-06-30 00:00:00.000' AS DateTime))
```

# STEP-2 : Create the Application
In this step, we will select the “ASP.NET Core Web API” project type.
Here we will select Framework type as .NET 6.0 and also select the ASP.NET Core hosted option.

# STEP-3 : Install Required Nuget Packages
Go to the “Tools” menu, select NuGet Package Manager > Package Manager Console and then run the below commands to add database provider and Entity Framework Tools.

=> Install-Package Microsoft.EntityFrameworkCore
=> Install-Package Microsoft.EntityFrameworkCore.SqlServer
=> Install-Package Microsoft.AspNetCore.Authentication.JwtBearer

# STEP-4 : Adding the Model to the Application
Now we will create two Model classes that will contain the UserInfo and Employee model properties.

To do that right-click on the “Authentication_Authorization_core” project and add a New Folder as “Models”.

Then right-click on the “Models” folder and add two classes as “UserInfo.cs” and “Employee.cs”.

Now open the “UserInfo.cs” file and paste the code to it.

### Now open the “Employee.cs” file and paste the code to it.

# STEP-5 : Adding Data Access Layer to the Application:
Now we will create a “DatabaseContext.cs” class where we define database connection. To do that right-click on the “Authentication_Authorization_core” project and add a folder as “Models”. Add the “DatabaseContext.cs” file to the “Models” folder and put the below to it.

##### Now we will create another two folders “Interface” and “Repository” to handle database-related operations.

Right-click on the “JWTAuth.WebApi” project and add two new folders as “Interface” and “Repository”.

Now add an interface to the “Interface” folder, name it as “IEmployees.cs” and put the below code to it.

#####  Now add a class name as “EmployeeRepository.cs” to the “Repository” folder, which will inherit “IEmployees” interface, and put the below code to it.

##### Now we will add “DatabaseContext”,“IUser” and “UserManager” reference to the “Program.cs” file of the“Authentication_Authorization_core” project.

Open the “Program.cs” file and put the code to it.

# STEP-6 : Adding the Web API Controller to the Application

Right-click on the “Controllers” folder and select “Add” then “New Item”. It will open an “Add New Item” dialog box. Select “ASP.NET” from the left panel, then select “API Controller - Empty” from templates and put the controller class name as “EmployeeController.cs”. Press Add to create the controller.
Now open the “EmployeeController.cs” file and put the code into it.

# STEP-7 : Run the Application and Test APIs with Postman
Before we execute the application, change the lunch URL to “api/employee” in “launchSettings.json”. When we execute the application will be able to see all employee listings like the below image.

### Now we will see how to consume our service using Postman.

Postman is an API testing tool that helps developers consume and check how an API works. You can download and install Postman here.

## To view the Employee list

Step 1

Open Postman and enter this endpoint:  https://localhost:7113/api/employee. 

Step 2 

Choose the method as GET and click Send.

### To view the details of an Employee

Step 1

Open Postman and enter this endpoint: https://localhost:7113/api/employee/1.

Step 2

Choose method as GET and click Send. Now, you can see the details of the employee.

#To create a new employee

Step 1

Enter this endpoint into Postman: https://localhost:7113/api/employee.

Step 2

Choose the POST method and under Body > Raw, choose type JSON and paste the employee details. By clicking Send, a new employee is created.

#To update details of an employee

Step 1

Enter this endpoint into Postman: https://localhost:7113/api/employee/5.

Step 2

Choose the PUT method and under Body > Raw, choose type JSON and paste the employee details to update. By clicking on Send, the details are updated.

#To delete an employee

Step 1

Enter this endpoint into Postman: https://localhost:7113/api/employee/12.

Step 2

Choose the DELETE method and click Send. Now, the employee details will be deleted from the database.

## fOR THE AUTHORIZATION STEPS CHECK Follow steps2.md 
