---
layout: default
title: Dapper 
permalink: dapper
---

{% include template-h1.html %}

## What's Dapper?
Dapper is a simple object mapper for .NET and own the title of **King of Micro ORM** in terms of speed and is virtually as fast as using a raw ADO.NET data reader. An ORM is an Object Relational Mapper, which is responsible for mapping between database and programming language.

Dapper extend the IDbConnection by providing useful extension methods to query your database.

## How Dapper Works?
It is a three step process.
- Create an IDbConnection object.
- Write a query to perform CRUD operations.
- Pass query as a parameter in Execute method. 

## Installation
Dapper is installed through NuGet: <a href="https://www.nuget.org/packages/Dapper" target="_blank">https://www.nuget.org/packages/Dapper</a>

> PM> Install-Package Dapper

## Requirement
Dapper work with any database provider since there is no DB specific implementation.

## Methods
Dapper will extend your IDbConnection interface with multiple methods:

- [Execute](/execute)
- [Query](/query)
- [QueryFirst](/queryfirst)
- [QueryFirstOrDefault](/queryfirstordefault)
- [QuerySingle](/querysingle)
- [QuerySingleOrDefault](/querysingleordefault)
- [QueryMultiple](/querymultiple)

{% include template-example.html %} {% highlight csharp %}
string sqlOrderDetails = "SELECT * FROM OrderDetails;";
string sqlOrderDetail = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";
string sqlCustomerInsert = "INSERT INTO Customers (CustomerName) Values (@CustomerName);";


using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	var orderDetails = connection.Query(sqlOrderDetails).ToList();
	var orderDetail = connection.QueryFirstOrDefault(sqlOrderDetail, new {OrderDetailID = 1});
	var affectedRows = connection.Execute(sqlCustomerInsert,  new {CustomerName = "Mark"});
}
{% endhighlight %}

{% include component-try-it.html href='https://dotnetfiddle.net/vIvUNm' %}

## Parameter
Execute and queries method can use parameters from multiple different ways:

- [Anonymous](/parameter-anonymous)
- [Dynamic](/parameter-dynamic)
- [List](/parameter-list)
- [String](/parameter-string)

{% include template-example.html %} {% highlight csharp %}
// Anonymous
var affectedRows = connection.Execute(sql,
                    new {Kind = InvoiceKind.WebInvoice, Code = "Single_Insert_1"},
                    commandType: CommandType.StoredProcedure);

// Dynamic
DynamicParameters parameter = new DynamicParameters();

parameter.Add("@Kind", InvoiceKind.WebInvoice, DbType.Int32, ParameterDirection.Input);
parameter.Add("@Code", "Many_Insert_0", DbType.String, ParameterDirection.Input);
parameter.Add("@RowCount", dbType: DbType.Int32, direction: ParameterDirection.ReturnValue);

connection.Execute(sql,
	new {Kind = InvoiceKind.WebInvoice, Code = "Single_Insert_1"},
	commandType: CommandType.StoredProcedure);

// List
connection.Query<Invoice>(sql, new {Kind = new[] {InvoiceKind.StoreInvoice, InvoiceKind.WebInvoice}}).ToList();

// String
connection.Query<Invoice>(sql, new {Code = new DbString {Value = "Invoice_1", IsFixedLength = false, Length = 9, IsAnsi = true}}).ToList();
{% endhighlight %}

## Result
The result returned by queries method can be mapped to multiple types:

- [Anonymous](/result-anonymous)
- [Strongly Typed](/result-strongly-typed)
- [Multi-Mapping](/result-multi-mapping)
- [Multi-Result](/result-multi-result)
- [Multi-Type](/result-multi-type)

{% include template-example.html %} {% highlight csharp %}
string sqlOrderDetails = "SELECT * FROM OrderDetails;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	var anonymousList = connection.Query(sqlOrderDetails).ToList();
	var orderDetails = connection.Query<OrderDetail>(sqlOrderDetails).ToList();
}
{% endhighlight %}

{% include component-try-it.html href='https://dotnetfiddle.net/EbR9BP' %}

## Utilities

- [Async](async)
- [Buffered](buffered)
- [Transaction](transaction)
- [Stored Procedure](stored-procedure)

{% include template-example.html %} {% highlight csharp %}
// Async
connection.QueryAsync<Invoice>(sql)

// Buffered
connection.Query<Invoice>(sql, buffered: false)

// Transaction
using (var transaction = connection.BeginTransaction())
{
	var affectedRows = connection.Execute(sql,
		new {Kind = InvoiceKind.WebInvoice, Code = "Single_Insert_1"},
		commandType: CommandType.StoredProcedure,
		transaction: transaction);

	transaction.Commit();
}

// Stored Procedure
var affectedRows = connection.Execute(sql,
	new {Kind = InvoiceKind.WebInvoice, Code = "Single_Insert_1"},
	commandType: CommandType.StoredProcedure);
{% endhighlight %}
