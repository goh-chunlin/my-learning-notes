# Views

The View is responsible for providing the user interface (UI) to the user.

Unlike file-based web frameworks, such as ASP.NET Web Forms and PHP, Views are not themselves directly accessible. So, a View is always rendered by a Controller, which provides the data the View will render. More often, the Controller needs to pass a data transfer object called a Model to provide some information to the View, so it . The View transforms that Model into a format ready to be presented to the user. 

## View Conventions
A Views directory structured in a very specific manner. In the Views directory, there are folders corresponding to the Controllers. Each Controller folder contains a View file for each Action method. The View file is named the same as the Action method.

## ViewBag, ViewData, and ViewDataDictionary
Technically, all data is passed from the controllers to the Views via a ViewDataDictionary (a specialized dictionary class) called ViewData. We can set and read values to the ViewData dictionary using standard dictionary syntax, as follows:

```
ViewData["WelcomeMessage"] = "Hello!";
```

Starting from ASP.NET MVC 3, the C# 4 dynamic keyword is leveraged to allow for a simpler syntax by using ViewBag. ViewBag is a dynamic wrapper around ViewData. It allows you to set values as follows:

```
ViewBag.WelcomeMessage = "Hello!";
```

One important thing to note is that dynamic values cannot be passed as parameters to extension methods. The C# compiler must know the real type of every parameter at compile time in order to choose the correct extension method. If any parameter is dynamic, compilation will fail. For example, this code will always fail: ```@Html.TextBox("name", ViewBag.WelcomeMessage)```. To work around this, either use ```ViewData["WelcomeMessage"]``` or cast the value to a specific type: ```(string)ViewBag.WelcomeMessage```.

## View Models
Often a View needs to display a variety of data that doesn't map directly to a domain model.

One easy approach to displaying extra data that isn't a part of the View's main Model is to simply stick that data in the ViewBag.

Another recommended approach is to write a custom View Model (VM) class. VM can be considered as a Model that exists just to supply information for a View. Note that the term View Model here is different from the concept of view model within the MVVM pattern.

```
public class SalesReportVM {   
    public IEnumerable<RetailBooking> RetailBookings { get; set; }   
    
    public decimal TotalSales { get; set; }   
    
    public string ReportType { get; set; }
    
    public DateTime ReportStartDate { get; set; } 
    
    public DateTime ReportEndDate { get; set; } 
}
```
