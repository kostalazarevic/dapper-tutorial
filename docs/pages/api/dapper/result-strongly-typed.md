---
layout: default
title: Dapper - Result Strongly Typed 
permalink: result-strongly-typed
---

{% include template-h1.html %}

## Description
Extension methods can be used to execute a query and map the result using strongly typed.

The anonymous result can be mapped from following methods:

- [Query](#example---query)
- [QueryFirst](#example---queryfirst)
- [QueryFirstOrDefault](#example---queryfirstordefault)
- [QuerySingle](#example---querysingle)
- [QuerySingleOrDefault](#example---querysingleordefault)

These extension methods can be called from any object of type IDbConnection.
## Example - Query
Query method can execute a query and map the result to a strongly typed list.

{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetails = connection.Query<OrderDetail>(sql).ToList();

	Console.WriteLine(orderDetails.Count);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/dXZc0s' %}

## Example - QueryFirst
QueryFirst method can execute a query and map the first result to a strongly typed list.

{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QueryFirst<OrderDetail>(sql, new {OrderDetailID = 1});

	Console.WriteLine(orderDetail.Quantity);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/AV0OgZ' %}

## Example - QueryFirstOrDefault
QueryFirstOrDefault method can execute a query and map the first result to a strongly typed list, or a default value if the sequence contains no elements.

{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QueryFirstOrDefault<OrderDetail>(sql, new {OrderDetailID = 1});

	Console.WriteLine(orderDetail.Quantity);
}
{% endhighlight %}

{% include component-try-it.html href='https://dotnetfiddle.net/2WQ7sc' %}

## Example - QuerySingle
QuerySingle method can execute a query and map the first result to a strongly typed list, and throws an exception if there is not exactly one element in the sequence.

{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QuerySingle<OrderDetail>(sql, new {OrderDetailID = 1});

	Console.WriteLine(orderDetail.OrderDetailID);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/vnkv7q' %}

## Example - QuerySingleOrDefault
QuerySingleOrDefault method can execute a query and map the first result to a strongly typed list, or a default value if the sequence is empty; this method throws an exception if there is more than one element in the sequence.

{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QuerySingleOrDefault<OrderDetail>(sql, new {OrderDetailID = 1});

	Console.WriteLine(orderDetail.OrderDetailID);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/kFMKnL' %}
