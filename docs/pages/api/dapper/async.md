---
layout: default
title: Dapper - Async
permalink: async
---

{% include template-h1.html %}

## Description
Dapper also extend the IDbConnection interface with Async (asynchronous) methods:
- [ExecuteAsync](#executeasync)
- [QueryAsync](#queryasync)
- [QueryFirstAsync](#queryfirstasync)
- [QueryFirstOrDefaultAsync](#queryfirstordefaultasync)
- [QuerySingleAsync](#querysingleasync)
- [QuerySingleOrDefaultAsync](#querysingleordefaultasync)
- [QueryMultipleAsync](#querymultipleasync)

> We only added non-asynchronous version in this tutorial to make it easier to read.

## ExecuteAsync

{% include template-example.html %} {% highlight csharp %}
string sql = "INSERT INTO Customers (CustomerName) Values (@CustomerName);";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	var affectedRows = connection.ExecuteAsync(sql, new {CustomerName = "Mark"}).Result;
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/2rVSi0' %}

## QueryAsync
{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetails = connection.QueryAsync(sql).Result.ToList();

	Console.WriteLine(orderDetails.Count());
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/X79bZI' %}

## QueryFirstAsync
{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QueryFirstAsync<OrderDetail>(sql, new {OrderDetailID = 1}).Result;

	Console.WriteLine(orderDetail);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/7Jbdcg' %}

## QueryFirstOrDefaultAsync
{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QueryFirstOrDefaultAsync<OrderDetail>(sql, new {OrderDetailID = 1}).Result;

	Console.WriteLine(orderDetail.Quantity);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/26NWaz' %}

## QuerySingleAsync
{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QuerySingleAsync<OrderDetail>(sql, new {OrderDetailID = 1}).Result;

	Console.WriteLine(orderDetail.OrderDetailID);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/pmjYFp' %}

## QuerySingleOrDefaultAsync
{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails WHERE OrderDetailID = @OrderDetailID;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetail = connection.QuerySingleOrDefaultAsync<OrderDetail>(sql, new {OrderDetailID = 1}).Result;

	Console.WriteLine(orderDetail.OrderDetailID);
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/WvbA02' %}

## QueryMultipleAsync
{% include template-example.html %} {% highlight csharp %}
var sql = "SELECT * FROM Invoice; SELECT * FROM InvoiceItem;";

using (var connection = My.ConnectionFactory())
{
	connection.Open();

	using (var multi = connection.QueryMultipleAsync(sql, new { InvoiceID = 1 }).Result)
	{
		var invoice = multi.Read<Invoice>().First();
		var invoiceItems = multi.Read<InvoiceItem>().ToList();
	}
}
{% endhighlight %}


