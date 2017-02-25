# Models

The word *model* in software development is overloaded to cover many different concepts. Even in ASP .NET MVC context alone, it has two diffent meanings, i.e.
 1. Business-oriented model object;
 2. View-specific model object.

## What Is Scaffolding?
Scaffolding in ASP .NET MVC can generate the boilerplate code we need for CRUD functionality in the web app. The scaffolding templates can examine the type definition for a Model, and then generate a Controller, Views associated with the Controller, and, in some cases, data access classes as well.

The scaffolding knows how to name Controllers, how to name Views, what code needs to go in each component, and where to place all these pieces in the project for the application to work. Hence, scaffolding helps the developers to not waste their time working on boring work of creating files in the right directories by hand.

Developers are allowed to customize or even replace the default scaffolding behavior to fullfill their own needs. In addition, alternatives scaffolding templates are available in NuGet repository.

## Scaffolding and Entity Framework (EF)
A new ASP .NET MVC 5 project automatically includes a reference to EF, the Object-Relational Mapping (ORM) framework. EF understands how to store .NET objects in a relational database and retrieve those same objects given a LINQ query.

EF supports three major styles.
 - Code First;
 - Database First;
 - Model First.
 
## EF and Code First
Code First means we can start storing and retrieving information in database without creating a database schema. Instead, we write plain C# classes and EF will figure out how and where to store the instances of those classes.

Normally, the properties in our Models are virtual.

```
public class RetailBooking
{
    public virtual int ID { get; set; }
    
    public virtual string OrderNumber { get; set; }
    
    public virtual DateTime JourneyDateTime { get; set; }
    
    public virtual string Origin { get; set; }
    
    public virtual string Destination { get; set; }

}
```

Virtual properties are not required, but they do give EF a hook into our plain C# classes and enable features such as an efficient change-tracking mechanism. The EF needs to know when a property value on a model changes, because it might need to issue a SQL UPDATE statement to reconcile those changes with the database.

## Code First Conventions
EF follows a number of conventions.
 - If we store an object of type *RetailBooking* in the database, EF will store the data in a table named *RetailBookings* (Yup, it become plural form!).
 - If we have a property on the Model named ID, EF will assume the property holds the primary key value and set up an auto-incrementing key column in the database to hold the property value.
 
Sometimes these default conventions are not ideal for our Model. Starting from EF 6 onwards, we can use [Custom Code First Conventions](https://msdn.microsoft.com/en-us/library/jj819164(v=vs.113).aspx) to define our own conventions that provide configuration defaults for our Model. So, for example, if we don't want EF to store the data of object with type *RetailBooking* in a table named *RetailBookings*, instead we want the table to be called *Transactions*, then we can do as follows.

```
public class RetailContext : DbContext
{
    ...
    protected override void OnModelCreating(DbModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);
        
        modelBuilder.Entity<RetailBooking>().ToTable("Transactions");
    }
    
    public DbSet<RetailBooking> RetailBookings { get; set; }
    
    ...
}
```

##The DbContext Class
As what is shown above, the gateway to the database is a class derived from EF's DbContext class.

The derived class *RetailContext* has one or more properties of type DbSet<T>, where each T represents the type of the object we want to persist. For example, the following RetailDbContext class allows us to store and retrieve RetailBooking information.

```
public class RetailDbContext : DbContext
{
    ...
    
    public DbSet<RetailBooking> RetailBookings { get; set; }
    
    ...
}
```

So by using RetailDbContext, we can, for example, retrieve all bookings having JourneyDateTime in 2017 using LINQ as shown below.

```
using (var db = new RetailDbContext()) {

    var desiredBookings = db.RetailBookings.Where(b => b.JourneyDate.Year == 2017).ToList();
    
    ...
}
```

## Creating Database with EF
The Code First approach of EF will create a database for us using a convention if we do not configure a specific database connection to use at runtime.

To explicitly configure a connection for a Code First data context, we just need to add a connection string to the web.config file. By convention, EF will look for a connection string with a name matching the name of the data context class.

```
<connectionStrings>
    <add name="RetailConnection" connectionString="..." providerName="System.Data.SqlClient" />
</connectionStrings>
```

## Data Migration
Introduced in EF 4.3, Data Migration is a systematic, code-based method for applying changes to the database. Data Migration allows existing data in the database to be preserved as the Model definitions are built and refined. So when there is a change in Model, EF can track those changes and create migration scripts that can be applied to the database.

To detect changes in the Model, EF is using the records stored in a table called *__MigrationHistory*. The table __MigrationHistory is created by EF. It stores a compressed version of the Code First Model for each Data Migration. When the Model is changed, for example by adding a property, EF will use the information stored in the __MigrationHistory table to determine what has changed. By doing so, it allows developers to migrate the database between versions as desired.

Developers are allowed to delete the __MigrationHistory table. However, this means that developers or DBAs will be responsible for making database schema changes to match the changes in the Model.

To enable Data Migration, we need to enter the following command in the Package Manager Console window in Visual Studio.

```
> Enable-Migration
```

This command adds a folder named Migrations to your project, plus a code file named **Configuration.cs** in the Migrations folder.

Data Migration supports seed methods which allow us to create some initial data for the application. To do so, we need to add the following code to the **Seed** method in the **Configuration.cs**.

```
protected override void Seed(RetailDbContext context)
{
     //  This method will be called after migrating to the latest version.

     //  You can use the DbSet<T>.AddOrUpdate() helper extension method 
     //  to avoid creating duplicate seed data. E.g.
     //
     //    context.People.AddOrUpdate(
     //      p => p.FullName,
     //      new Person { FullName = "Andrew Peters" },
     //      new Person { FullName = "Brice Lambson" },
     //      new Person { FullName = "Rowan Miller" }
     //    );
     //
}
```

## Model Binding
Let's say we have implemented the Edit action for an HTTP POST and we know that Edit view will post Form values to the server. If we want to retrieve those submitted values, we can directly pull them from the Request.

```
[HttpPost]
public ActionResult Edit() 
{
    var retailBooking = new RetailBooking();
    
    retailBooking.OrderNumber = Request.Form["OrderNumber"];
    retailBooking.JourneyDateTime = Convert.ToDateTime(Request.Form["JourneyDateTime"]);
    ...
}
```

Alternatively, we can improve the code maintainability by using Model Binding feature offered in ASP .NET MVC.

Instead of digging form values out of the request, the Edit action simply takes an RetailBooking object as a parameter.

```
[HttpPost]
public ActionResult Edit(RetailBooking retailBooking) 
{
    ...
}
```

The default model binder inspects the RetailBooking and finds all the RetailBooking properties available for binding. Following the naming convention, the default model binder can automatically convert and move values from the request into an RetailBooking object.

## Model Binding and Over-Posting Attack
Sometimes the aggressive search behavior of the model binder can have unintended consequences. Occasionally there is a property we don't want (or expect) the model binder to set. Thus, we need to be careful to avoid an [**Over-Posting Attack**](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost).

There are two ways to protect against the attack.
 - Bind: Use the *Include* parameter with the *Bind* attribute to whitelist fields that we allow to change.
 
 ```
 [HttpPost]
 public ActionResult Edit([Bind(Include="ID, OrderNumber, JourneyDateTime")]RetailBooking retailBooking) 
 {
     ...
 }
 ```
 
 - View Model: Use view models rather than entity classes with model binding. Include only the properties we want to update in the view model.
