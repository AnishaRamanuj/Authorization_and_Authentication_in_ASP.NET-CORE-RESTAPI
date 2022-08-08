# Authorization_and_Authentication_in_ASP.NET-CORE-RESTAPI

In this article, we are going to create a web application using .Net 6.0 and ASP.Net Core and also implement JWT Authentication.

JWT stands for JSON Web Token digitally signed using a secret key by a token provider. It helps the resource server to verify the token data using the same secret key.

JWT consists of three parts:

1.  Header: encoded data of the token type and the algorithm used to sign the data.<br/>
2.  Payload: encoded data of claims intended to share.<br/>
3.  Signature: created by signing (encoded header + encoded payload) using a secret key.<br/><br/>
Here I am going to use Visual Studio 2022 and SQL Server 2015.


In this Repository, I create a REST API using .Net 6.0, ASP.NET Core, perform basic CRUD operations, create a JWT token, and secure the APIs. Hope this article will help the readers.

Happy Coding!!!
