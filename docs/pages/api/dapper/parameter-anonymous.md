---
layout: default
title: Dapper - Parameter Anonymous 
permalink: parameter-anonymous
---

{% include template-h1.html %}

## Description
Dapper make it simple & safe (SQL Injection) to use parameter by supporting anonymous type.

### Single
Execute a single time a SQL Command.

{% include template-example.html %} {% highlight csharp %}
string sql = "INSERT INTO Customers (CustomerName) Values (@CustomerName);";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();

	var affectedRows = connection.Execute(sql, new {CustomerName = "Mark"});

	Console.WriteLine(affectedRows);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/Z1iRIQ' %}  

### Many
Execute many times a SQL Command

{% include template-example.html %} {% highlight csharp %}
string sql = "INSERT INTO Customers (CustomerName) Values (@CustomerName);";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var affectedRows = connection.Execute(sql,
 		new[]
 		{
     		new {CustomerName = "John"},
     		new {CustomerName = "Andy"},
     		new {CustomerName = "Allan"}
 		}
	);

	Console.WriteLine(affectedRows);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/fvRKsY' %}  