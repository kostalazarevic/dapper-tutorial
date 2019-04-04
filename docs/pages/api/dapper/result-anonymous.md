---
layout: default
title: Dapper - Result Anonymous 
permalink: result-anonymous
---

{% include template-h1.html %}

## Description
Extension methods can be used to execute a query and map the result using dynamic.

The anonymous result can be mapped from following extension methods:

- [Query](#example---query)
- [QueryFirst](#example---queryfirst)
- [QueryFirstOrDefault](#example---queryfirstordefault)
- [QuerySingle](#example---querysingle)
- [QuerySingleOrDefault](#example---querysingleordefault)

These extension methods can be called from any object of type IDbConnection.
## Example - Query
Query method can execute a query and map the result to a dynamic list.

{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetails = connection.Query(sql).ToList();

	Console.WriteLine(orderDetails.Count);
}
{% endhighlight %}

{% include component-try-it.html href='https://dotnetfiddle.net/qTvEME' %}

## Example - QueryFirst
QueryFirst method can execute a query and map the first result to a dynamic list.

{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QueryFirst(sql, new {OrderDetailID = 1});

	Console.WriteLine(orderDetail.Quantity);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/eogWc1' %}

## Example - QueryFirstOrDefault
QueryFirstOrDefault method can execute a query and map the first result to a dynamic list, or a default value if the sequence contains no elements.

{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QueryFirstOrDefault(sql, new {OrderDetailID = 1});

	Console.WriteLine(orderDetail.Quantity);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/58YMxR' %}

## Example - QuerySingle
QuerySingle method can execute a query and map the first result to a dynamic list, and throws an exception if there is not exactly one element in the sequence.

{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QuerySingle(sql, new {OrderDetailID = 1});

	Console.WriteLine(orderDetail);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/uEq0HC' %}

## Example - QuerySingleOrDefault
QuerySingleOrDefault method can execute a query and map the first result to a dynamic list, or a default value if the sequence is empty; this method throws an exception if there is more than one element in the sequence.

{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QuerySingleOrDefault(sql, new {OrderDetailID = 1});

	Console.WriteLine(orderDetail);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/nYmbCo' %}
