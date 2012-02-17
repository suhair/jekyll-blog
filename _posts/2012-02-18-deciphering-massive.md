---
layout: post
title: Deciphering Massive
---

Deciphering the code behind Massive - the ultra lite ORM in c#
==============================================================

Provider Factories
------------------
.net framework unifies the disparage data providers under a common namespace called System.Data.Common.
Each provider has a different set of classes to represent the database functionality. 

To work independently of the provider, you can obtain the desired DbProviderFactory by passing the 
provider invariant name to the DbProviderFactories.GetFactory method. DbProviderFactories.GetFactoryClasses when
invoked will list all of the registered provider factories in the system.

When the DbProviderFactory is obtained in the above manner, all is set to create the desired data source classes like
Connection and Command. ExecuteReader method on the thus obtained command could be used for obtaining a DataReader. Read method
on the DataReader populates the DataReader object with the first row and returns a boolean value indicating whether more rows to read
further exists or not. So in effect Read could be called in a while loop and we can obtain the name and value inside each columns of the current
read row in the DataReader. GetName, and GetValue methods on the reader returns the name and value of the column(field) respectively if the column index is passed.
 

Expando Object
--------------

System.Dynamic namespace hosts ExpandoObject. ExpandoObject implements IDictionary<String, Object>. Since Expando object is synonymous to a dictionary with
key of type string and value of object, we can easily create a dynamic object by casting the newly created Expando object to a dictionary and then adding
the name value pairs obtained through enumerating the DataReader object. 
