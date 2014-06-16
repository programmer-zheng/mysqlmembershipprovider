MySql SimpleMembership Provider for ASP.NET MVC and WCF
=================================================


with Entity Framework 6.x CodeFirst
-----------------------------------

# License

Apache License 2.0

# Libraries
* MySql.Web.Extension : MySql SimpleMembership Provider for Entity Framework Code First

# Samples
* SimpleMembershipTest : ASP.NET MVC Simple Membership sample web site
* SimpleMembership.Dac : SimpleMembership Data access control


## MySql.Data.Extension Use only

> Install package by NuGet Package management 

  * Entity Framework 6.x above
  * MySql.Net 6.8.3 above

######  In app.config

```xml
<connectionStrings>
  <add name="SimpleMembershipConnection"
		 connectionString="server=localhost;port=3306;database=SimpleMembershipTest;User Id=dev;Password=thePassword;Persist Security Info=True;"
		 providerName="MySql.Data.MySqlClient" />
</connectionStrings>
```

```xml
  <entityFramework  codeConfigurationType="MySql.Data.Entity.MySqlEFConfiguration, MySql.Data.Entity.EF6">

  </entityFramework>
```

```xml
  <system.data>
	<DbProviderFactories>
	  <remove name="MySQL Data Provider" invariant="MySql.Data.MySqlClient" />
	  <add name="MySQL Data Provider" invariant="MySql.Data.MySqlClient" description=".Net Framework Data Provider for MySQL" 
	  type="MySql.Data.MySqlClient.MySqlClientFactory, MySql.Data, Version=6.8.3.0, Culture=neutral, PublicKeyToken=c5687fc88969c44d" />
	</DbProviderFactories>
  </system.data>
```

###### DbContext class inherited MySqlDbContext

```csharp
	public class MembershipDbContext : MySqlSecurityDbContext
	{
		public MembershipDbContext()
			: base("SimpleMembershipConnection")//Connection string defined in config
		{

		}
	}
```

###### Grant privileges to user

> mysql --user=root -p

> grant all privileges on SimpleMembershipTest.* to 'dev'@'%' identified by 'thePassword' with grant option;<br/>
> -- grant all privileges on **&lt;Database name&gt;**.* to '**&lt;UserName&gt;**'@'%' identified by '**&lt;UserPassword&gt;**' with grant option;

> flush privileges;

> use mysql;

> -- verify results<br/>
> select host, user from user where user = 'dev';<br/>
> select host, user, db from db where user = 'dev';


## MySql.Web.Extension Use

Step 1.
> Install package by NuGet Package management 

  * Entity Framework 6.x above
  * MySql.Net 6.8.3 above
  * Microsoft ASP.NET Razor 2
  * Microsoft ASP.NET Web Pages 2
  * Microsoft ASP.NET Web Pages 2 Data
  * Microsoft ASP.NET Web Pages 2 Web Data
  * Microsoft.Web.Infrastructure

Step 2.
> Reference MySql.Data.Extension project 

Step 3.

######  In web.config

```xml
<appSettings>
	<add key="enableMySqlSimpleMembership" value="true" />
	<add key="mySqlSecurityInheritedContextType" value="SimpleMembershipTest.Dac.SimpleMembershipTestDbContext, SimpleMembershipTest.Dac" />
</appSettings>
```
* "mySqlSecurityInheritedContextType" is System.Type.Name and non argument public constructor need.
<br/>

```xml
<connectionStrings>
  <add name="SimpleMembershipTestDbContext"
		 connectionString="server=localhost;port=3306;database=SimpleMembershipTest;User Id=dev;Password=thePassword;Persist Security Info=True;"
		 providerName="MySql.Data.MySqlClient" />
</connectionStrings>
```

```xml
<system.web>
	<membership defaultProvider="MySqlSimpleMembershipProvider">
		<providers>
			<clear />
			<add name="MySqlSimpleMembershipProvider"
				 type="MySql.Web.Security.MySqlSimpleMembershipProvider, MySql.Web.Extension" />
		</providers>
	</membership>

	<roleManager enabled="true" defaultProvider="MySqlSimpleRoleProvider">
		<providers>
			<clear />
			<add name="MySqlSimpleRoleProvider"
				 type="MySql.Web.Security.MySqlSimpleRoleProvider, MySql.Web.Extension" />
		</providers>
	</roleManager>
</system.web>
```


```xml
<system.data>
	<DbProviderFactories>
		<remove invariant="MySql.Data.MySqlClient" />
		<add name="MySQL Data Provider"
			 invariant="MySql.Data.MySqlClient"
			 description=".Net Framework Data Provider for MySQL"
			 type="MySql.Data.MySqlClient.MySqlClientFactory, MySql.Data, Version=6.6.4.0, Culture=neutral, PublicKeyToken=c5687fc88969c44d" />
	</DbProviderFactories>
</system.data>
```

###### DbContext class inherited MySecuritySqlDbContext

Inherited MySqlSecurityDbContext class that generate below tables.

  * UserProfile
  * WebPages_Membership
  * WebPages_OAuthMembership
  * WebPages_OAuthToken
  * WebPages_Rroles
  * WebPages_UsersInRoles
  * RoleMemberships



# Sample Project Screenshot

###### Add UserProperties

* Email
* Facebook
* Age
* Rate
* LastName
* FirstName

###### Support External login


# Special thanks

* Ki Won Kim's works at https://github.com/xyz37/MySqlSimpleMembershipProvider
* *Microsoft*, ASP.NET WebStack Source Code: http://aspnetwebstack.codeplex.com/
* Use SimpleMembership and OAuth with mySQL and bigint or any database and datatype you want: http://fabiocanada.ca/2012/11/24/use-simplemembership-and-oauth-with-any-database-and-datatype/
* Using Simple Membership Provider with mysql: http://stackoverflow.com/questions/12620922/using-simple-membership-provider-with-mysql
* Using Entity Framework Code First with MySQL: http://brice-lambson.blogspot.kr/2012/05/using-entity-framework-code-first-with.html
* Code First Migrations: Making __MigrationHistory not a system table: http://blog.oneunicorn.com/2012/02/27/code-first-migrations-making-__migrationhistory-not-a-system-table/
* *Jerrie Pelser*, Customizing External Login Buttons in ASP.NET MVC 4: http://www.beabigrockstar.com/customizing-external-login-buttons-in-asp-net-mvc-4/
