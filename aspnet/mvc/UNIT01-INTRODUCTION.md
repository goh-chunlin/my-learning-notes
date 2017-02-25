# Introduction to ASP .NET MVC

## About ASP .NET MVC
ASP .NET MVC is a framework for building web apps using general Model-View-Controller (MVC) pattern in ASP .NET framework.

* Model: A set of classes representing the domain of the web app and encapsulating data stored in database. Normally it uses Entity Framework with custom code containing domain-specific logic;
* View: User interface of the web app;
* Controller: A set of classes managing relationship between Model and View. In the web app, it responses to user input, talks to the Model, and decides whivh View (if any) to render.

ASP .NET MVC relies on many of the core strategies as follows.

* Convention over configuration;
* DRY Principle: Don't Repeat Yourself;
* Pluggability wherever possible.

## Razor View
Razor is introduced in ASP .NET MVC 3 as a new View Engine Syntax. The benefit of it is to focus on code-focused templating for HTML generation.

Before Razor, Web Form View Engine is used. So to write a for-each loop in View, we need to do as follows.

```
<ul>
    <% foreach (var user in Model.Users) { %>
    <li><%: user.Name %></li>
    <% } %>
</ul>
```

With Razor, we can simplify it as such.

```
<ul>
    @foreach (var user in Model.Users) {
    <li>@user.Name</li>
    }
</ul>
```

Razor syntax is easier to type and also easier to read after removing the XML-like syntax found in Web Form View Engine.

## Bundling and Minification
Starting from ASP .NET MVC 4, bundling and minification framework is supported.

Thanks to the framework, we can now reduce requests to our web app by combining several individual JS/CSS references into a single request. At the same time, it also helps to minify the requests by shortening variable names as well as removing comments and whitespaces in JS/CSS files.

By using bundling and minification, we can then remove actual JS/CSS file references from the View code. This means we can update JS/CSS files without the need to touch View codes.

## ASP .NET Scaffolding
Scaffolding is the process of generating boilerplate code based on your model classes. 

## ASP .NET MVC Convention over Configuration
ASP .NET MVC web apps, by default, rely heavily on conventions. This helps developers to avoid having to configure and specify things that can be inferred based on convention.

For example, ASP.NET MVC looks for the View template file within the \Views\ [ControllerName]\directory underneath the web app.

MVC is designed around some sensible convention-based defaults that can be overridden as needed. This concept is commonly referred to as **convention over configuration**.
