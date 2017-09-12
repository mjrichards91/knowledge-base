# Prism

[Prism](https://github.com/PrismLibrary/Prism) is an MVVM framework to be used with Xamarin development.

## Unit Testing

Unit Testing ViewModels is made easier with the Prism framework.

* Mock implementations of Dependency Interfaces
* Seed data using [fixtures](../../.NET/UnitTesting/Fixtures.md)

Example of a BaseTest class:

```csharp
/// <summary>
/// Base class to use for all view model tests.
/// </summary>
public abstract class BaseTest
{
    /// <summary>
    /// Gets the navigation service instance used for each test.
    /// </summary>
    public NavigationServiceMock NavigationService { get; private set; }

    /// <summary>
    /// Gets the dialog service instance used for each test.
    /// </summary>
    public PageDialogServiceMock DialogService { get; private set; }

    /// <summary>
    /// Creates the fixture for the given type. Recursive references are ignored.
    /// </summary>
    /// <typeparam name="T">The type to create.</typeparam>
    /// <returns>An instance of the provided type.</returns>
    public static T CreateFixture<T>()
    {
        Fixture fixture = new Fixture();

        // Prevent exceptions from being thrown for recursive references. See: 
        // https://github.com/AutoFixture/AutoFixture/wiki/Examples-of-using-behaviors#omitonrecursionbehavior 
        fixture.Behaviors
            .OfType<ThrowingRecursionBehavior>()
            .ToList()
            .ForEach(b => fixture.Behaviors.Remove(b));

        fixture.Behaviors.Add(new OmitOnRecursionBehavior());

        return fixture.Create<T>();
    }

    /// <summary>
    /// Set up for each test.
    /// </summary>
    public virtual void SetUp()
    {
        this.NavigationService = new NavigationServiceMock();
        this.DialogService = new PageDialogServiceMock();
    }
}
```
