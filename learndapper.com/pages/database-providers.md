---
title: Dapper Database Providers - SQL Server - Oracle - MySQL - PostgreSQL
description: Discover how to use Dapper database providers like SQL Server, MySQL, PostgreSQL, Oracle, and more on your website. Learn to install and apply these providers.
canonical: /database-providers
status: Published
lastmod: 2023-08-01
---

# Database Providers With Dapper

Dapper supports a variety of database providers, including the popular Microsoft SQL Server, Oracle, MySQL, PostgreSQL, SQLite, etc. 

 - It is important to note that Dapper does not provide any database abstraction layer like Entity Framework or NHibernate. 
 - Instead, it provides the user with several methods and extension points to extend the library for their custom database provider. 
 - This is possible because it uses the simple ADO.NET data providers that come with the .NET framework, so it can easily work with any existing database technology that supports ADO.NET. 
 - Dapper provides asynchronous support for all databases supported in ADO.NET. 
 - It also provides a range of powerful features, such as parameterized queries and native commands for all major database engines.

## Dapper SQL Server

Using Dapper to query SQL Server is straightforward. The first step is to install [Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient) NuGet package. You can also do it through the Nuget Package Manager Console by typing the following command.

```csharp
PM> NuGet\Install-Package Microsoft.Data.SqlClient
``` 

Using Dapper to access SQL Server is relatively easy. You first create a connection and start using methods from Dapper available.

```csharp
// Connect to the database 
using (var connection = new SqlConnection(connectionString)) 
{    
    // Create a query that retrieves all books with an author name of "John Smith"    
    var sql = "SELECT * FROM Books WHERE Author = @authorName";     
	
    // Use the Query method to execute the query and return a list of objects    
    var books = connection.Query<Book>(sql, new { authorName = "John Smith"}).ToList(); 
}
```

Once you have created the connection, you can use any [Dapper Query](/dapper-query/selecting-multiple-rows#dapper-query) methods to map the data returned from your query into a strongly typed object (or any other supported [querying methods](/dapper-query)). In addition, it includes [executing stored procedures](/stored-procedures) to retrieve data from the database.

## Dapper Oracle

To start using Oracle with Dapper, you must install the [Oracle.ManagedDataAccess.Core](https://www.nuget.org/packages/Oracle.ManagedDataAccess.Core) NuGet package.

Once the connection is created, you can begin writing code that uses Dapper's built-in methods for interacting with the database. These include [Execute](/non-query), [Execute Reader](/execute-reader), etc.

```csharp
// Connect to the database 
using (var connection = new OracleConnection(connectionString)) 
{    
    // Create a query that retrieves all books with an author name of "John Smith"    
    var sql = "SELECT * FROM Books WHERE Author=@authorName";     

    // Use the Query method to execute the query and return a list of objects    
    var books = connection.Query<Book>(sql, new {authorName="John Smith"}).ToList(); 
}
```

## Dapper SQLite

Dapper offers an easy way to access and manipulate data in an SQLite database. With its simple API and powerful features, Dapper can significantly reduce the amount of code needed to perform these tasks. As a result, it is an excellent choice for working with small datasets or prototyping applications. 

To start using SQLite with Dapper, you must install the [System.Data.SQLite.Core](https://www.nuget.org/packages/System.Data.SQLite.Core) NuGet package.


Using Dapper, you can connect to an SQLite database using a connection string like this: 

```csharp
private static string connectionString = "Data Source=D:\\BookStoreContext.db;";
```

To execute any SQL statement, such as returning the first author found by using [QueryFirst](/dapper-query/selecting-single-rows#dapper-queryfirst) or [QuerySingle](/dapper-query/selecting-single-rows) if only a single row is returned.

```csharp
// Connect to the database
using (var connection = new SQLiteConnection(connectionString))
{
    // Create a query that retrieves all authors"    
    var sql = "SELECT * FROM Authors LIMIT 1;";     

    // Use the Query method to execute the query and return the first author
    var author = connection.QueryFirst<Author>(sql).
}
```

## Dapper MySql

When working with MySQL in .NET Core, you must install the following NuGet package [MySql.Data](https://www.nuget.org/packages/MySql.Data).

Using Dapper to retrieve data from MySql is simple and can be done in a few lines of code. First, create a connection, then use any query method provided by Dapper, such as [ExecuteScalar](/dapper-query/selecting-scalar-values).

```csharp
// Connect to the database
using (var connection = new MySqlConnection(connectionString))
{
    // Create a query that retrieves all authors"    
    var sql = "SELECT * FROM Authors";     

    // Use the Query method to execute the query and return a list of objects
    List<Author> authors = connection.Query<Author>(sql).ToList();
}
```

## Dapper PostgreSQL

Dapper enables developers to easily and quickly query their PostgreSQL databases without writing complex SQL statements. 

 - With Dapper, developers can easily map data from Postgres tables into .NET objects in minutes.
 - This makes retrieving, storing, and manipulating data in PostgreSQL incredibly simple.

To start using PostgreSQL with Dapper, you must install the [Npgsql](https://www.nuget.org/packages/Npgsql) NuGet package.


```csharp
// Connect to the database
using (var connection = new NpgsqlConnection(connectionString))
{
    // Create a query that retrieves all authors"    
    var sql = "SELECT * FROM Authors";     

    // Use the Query method to execute the query and return a list of objects
    List<Author> authors = connection.Query<Author>(sql).ToList();
}
```

Like other providers, you must first create a connection and use any available Dapper methods, including [Dapper Bulk Operations](/bulk-operations) methods.

## Related Articles

- [Bulk Operations](/bulk-operations)