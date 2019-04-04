---
layout: default
title: Dapper - Buffered
permalink: buffered
---

{% include template-h1.html %}

## Description

- Default: True

A buffered query return the entire reader at once. That is ideal in most scenario.

A non-buffered query is equivalent as streaming. You only load objects on demand. That can be useful for a very large query to reduce memory usage.

{% include template-example.html %} {% highlight csharp %}
string sql = "SELECT * FROM OrderDetails;";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	var orderDetails = connection.Query<OrderDetail>(sql, buffered: false).ToList();

	Console.WriteLine(orderDetails.Count());
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/gLwGJO' %}
