This project is a fork of Mr Kim Ki Won's works at https://github.com/xyz37/MySqlSimpleMembershipProvider.

Major changes comparing with xyz37's works:
# Project MySql.Data.Extension was removed. This is because the functionality is already covered by MySql .NET libraries and Entity Framework 5/6.
# Fixed some minor bugs.
# Removed some redundant codes which are covered by ASP .NET Web Stack.
# Strong named.

Through maximizing the usage of MySql .NET libraries from Oracle and ASP .NET Web Stack, the project realizes the following:
# Minimum additional footprint for MVC applications in both codes and config. ASP .NET Web Stack is optimized for MS SQL while supporting the others, and the default settings are from MS SQL.
# Minimum codes different from WebMatrix.WebData, so the project could easily evolve with its MS SQL counterpart.


**Remarks**
If you start off a new project using VS 2013 or ASP .NET MVC 5, you may consider using ASP .NET Identity System, and there are quite a few articles in www.asp.net about the identity System on MySql Storage as well as this article "[Authentication and Authorization with ASP.NET Identity 2.0 for WCF Services](http://www.codeproject.com/Articles/802435/Authentication-and-Authorization-with-ASP-NET-Iden)"