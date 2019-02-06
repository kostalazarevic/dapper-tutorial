---
PermaID: 1000199
Name: Bulk Insert
---

# Dapper Plus - Bulk Insert

## Description
INSERT entities using Bulk Operation.

- [Insert single](#example---insert-single)
- [Insert many](#example---insert-many)
- [Insert with relation (One to One)](#example---insert-with-relation-one-to-one)
- [Insert with relation (One to Many)](#example---insert-with-relation-one-to-many)

## Example - Insert Single
INSERT a single entity with Bulk Operation.

```csharp
DapperPlusManager.Entity<Customer>().Table("Customers"); 

using (var connection = new SqlCeConnection("Data Source=SqlCe_W3Schools.sdf"))
{
	connection.BulkInsert(new List<Customer>() { new Customer() { CustomerName = "ExampleBulkInsert", ContactName = "Example Name :" +  1}});
}		
```
{% include component-try-it.html href='https://dotnetfiddle.net/d8Jxij' %}

## Example - Insert Many
INSERT many entities with Bulk Operation.

```csharp
DapperPlusManager.Entity<Customer>().Table("Customers"); 

using (var connection = new SqlCeConnection("Data Source=SqlCe_W3Schools.sdf"))
{
	connection.BulkInsert(customers);
}
```
{% include component-try-it.html href='https://dotnetfiddle.net/0rXZS9' %}

## Example - Insert with relation (One to One)
INSERT entities with a one to one relation with Bulk Operation.

```csharp	
DapperPlusManager.Entity<Supplier>().Table("Suppliers").Identity(x => x.SupplierID);
DapperPlusManager.Entity<Product>().Table("Products").Identity(x => x.ProductID);

using (var connection = new SqlCeConnection("Data Source=SqlCe_W3Schools.sdf"))
{	
	connection.BulkInsert(suppliers).ThenForEach(x => x.Product.SupplierID = x.SupplierID).ThenBulkInsert(x => x.Product);
}	
```
{% include component-try-it.html href='https://dotnetfiddle.net/9DMDMe' %}

## Example - Insert with relation (One to Many)
INSERT entities with a one to many relation with Bulk Operation.

```csharp	
DapperPlusManager.Entity<Supplier>().Table("Suppliers").Identity(x => x.SupplierID); 
DapperPlusManager.Entity<Product>().Table("Products").Identity(x => x.ProductID); 	

using (var connection = new SqlCeConnection("Data Source=SqlCe_W3Schools.sdf"))
{	
	connection.BulkInsert(suppliers).ThenForEach(x => x.Products.ForEach(y => y.SupplierID =  x.SupplierID)).ThenBulkInsert(x => x.Products);
}
```
{% include component-try-it.html href='https://dotnetfiddle.net/rzZDRy' %}
