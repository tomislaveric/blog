---
layout: post
title:  "Xamarin.Forms constructor injection with unity"
categories: recipes xamarin dependency-injection
---
A simple and straight forwared approach to get dependency injection, especially constructor injection, to work in Xamarin.Forms via Unity.

### Project setup
Open Visual Studio for Mac and create a `Multiplatform -> Blank Forms App`. Choose any name check `Android` and `iOS` for the target platforms, choose for Shared Code the `Portable Class Library` and check `use XAML for user interface files`. Click next for the next step and now lets jump right into it.

### Install unity container
One simple and easy way to use constructor injection in Xamarin.Forms is via unity. Do a right click on packages in your solution folder of the shared project and select `Add packages` and type `Unity`. NuGet will show you the unity package from author `Microsoft.Practices.Unity`, choose this one and select `Add Package`.

### Create the service to be injected
You have to create a `interface` and the corresponding `service`. Let's add a simple `DataService` to demonstrate the injection. First, create the interface `IDataService` and add the method `GetCities()` to it.

{% highlight csharp %}
public interface IDataService
{
    IEnumerable<string> GetCities();
}
{% endhighlight %}

Now let us create the DataService class with it's implemented interface.

{% highlight csharp %}
public class DataService : IDataService
{
    public IEnumerable<string> GetCities()
    {
        return new List<string>{
          "Karlsruhe",
          "Split",
          "Dubrovnik"
        };
    }
}
{% endhighlight %}

### Inject the service via construction injection
To consume the data fetched by the dataservice we have to inject the service in a viewmodel to demonstrate it. Create the `CityListViewModel` with a uninitialized private field of type `IDataService`. Now inject the service in the constructor. With this implementaion we will get a `NullReferenceException` because the DataService was not instantiated.

{% highlight csharp %}
public class CityListViewModel
{
    private readonly IDataService dataservice;

    public CityListViewModel(IDataService dataService)
    {
        this.dataservice = dataService;
    }

    public IEnumerable<string> AllCities => dataservice.GetCities();
}
{% endhighlight %}

### Setup the unity container
To prevent throwing NullReferenceException from last step, we have to setup a container to be able to use constructor injection in our shared code files. A good place to do this, is right after Xamarin.Forms initializes it's components. The initialization takes place at `App.xaml.cs` file. We just have to instatiate a `new UnityContainer` and register our types, next we have to tell the `ServiceLocator` to use our newly created container as the current `LocatorProvicer`. Finally we have to call our method from `App.xaml.cs`s constructor. And thats it!

{% highlight csharp %}
private void RegisterService()
{
    var unityContainer = new UnityContainer();
    unityContainer.RegisterType<IDataService, DataService>();
    // register any service you like with the scheme interface, service
    ServiceLocator.SetLocatorProvider(() => 
        new UnityServiceLocator(unityContainer));
}
{% endhighlight %}

Now our `CityListViewModel` will be able to get the list of cities without a NullRefereneException. This is how you can achieve a constructor injection in Xamarin.Forms.
