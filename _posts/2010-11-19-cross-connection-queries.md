---
title: "Cross Connection Queries"
date: 2010-11-19 18:45:00 +0000
last_modified_at: 2010-11-19 23:39:19 +0000
tags:
  - Bridge
  - SQL Developer
---

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgi5ej4IIqEdv8N5uKKe2mULKTtyuq0hJuz84ulpM8i5PsiThnI9TqMSxi2tIWLE4LaPSUPPlbXbbNCwUV7Tyaj97FeTnIGalERzdoQrVzfA6wdXsc6UPJqciSEw-JA7E3mcd2DwYRWjf4/s320/copytooracle.PNG)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgi5ej4IIqEdv8N5uKKe2mULKTtyuq0hJuz84ulpM8i5PsiThnI9TqMSxi2tIWLE4LaPSUPPlbXbbNCwUV7Tyaj97FeTnIGalERzdoQrVzfA6wdXsc6UPJqciSEw-JA7E3mcd2DwYRWjf4/s1600/copytooracle.PNG)[When we were hooking up the "Copy to Oracle" functionality,](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgi5ej4IIqEdv8N5uKKe2mULKTtyuq0hJuz84ulpM8i5PsiThnI9TqMSxi2tIWLE4LaPSUPPlbXbbNCwUV7Tyaj97FeTnIGalERzdoQrVzfA6wdXsc6UPJqciSEw-JA7E3mcd2DwYRWjf4/s1600/copytooracle.PNG) [Dermot](http://dermotoneill.blogspot.com/) added a cool bit of code to allow us to do queries across connections.

The Copy to Oracle function allows you point at a table in any supported connection type and choose copy to oracle from the menu. This then goes and creates the table in Oracle and populates it with data from the source table.

Now, as I said, to do this, [Dermot](http://dermotoneill.blogspot.com/) added some functionality to enable this. This functionality is very flexible and the UI in Copy to Oracle uses this mechanism to achieve the functionality.

The command shown here is just the basics of what this can do and we will document this in more detail as we go on.

BRIDGE DEMO\_CUSTOMERS AS access

(SELECT \* FROM "Order Details") ;

This command can be broken into a few pieces. After the BRIDGE token, the identifier is the name of the new table to be create in the current Oracle connection. The access identifier represents the connection that we will copy the table from and the query between the braces is the query which will be run on the source connection as the data for the new table.

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilQK4h87CbAZ97pYhoEgPkIuroLX-qwlOQ1e0yimhPFFa5_Z77FunqWf9XKoefYX6RTrI4jESQ-dXN-zLOEn5HAvgUj6hHZhyTAWi5nkYxdHdcFYJDOKWGsw96Mf-O3yKvbYZqIEdv6p8/s320/accesscopied.PNG)

Running the commands listed here, drop the table if it exists and creates it on the Oracle Connection.

We then run a query against that connection we get the following results in the results panel.

This is just a small view into what the bridge command can do and how it is used in the Copy to Oracle Functionality today.

Now we have the table is in Oracle. However, we can do something even cooler than this. We can join a table in Oracle with a table in Access and show the results.

BRIDGE TEMPcustomers AS access

(SELECT \* FROM "Order Details")

SELECT \* FROM TEMPcustomers,Products

where Products.productid=TEMPcustomers.ProductID;

This is a little step further. We take the table in Access, copy it to Oracle as a temporary table and join it with a table in Oracle to show the results below.

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhm8ZvfqrJgRjzi9ZT6CgeUycB3kn6gaiPbzxPEssOg-vo8OJMjcmzKIINuASrFPHjKLvsJr2hrAX5VwcGQt5CJWZoN2RqLJDE0Rhtt0gRw46XcXwv_xE6i3swnbyh559HnG8w_NQEtLSo/s320/bridgejoin.PNG)
