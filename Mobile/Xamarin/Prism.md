# Prism

[Prism](https://github.com/PrismLibrary/Prism) is an MVVM framework to be used with Xamarin development.

## Unit Testing

Unit Testing ViewModels is made easier with the Prism framework.

* Mock implementations of Dependency Interfaces
* Seed data using [fixtures](../../.NET/UnitTesting/Fixtures.md)

### BaseTest Class

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

### Mock NavigationService

Mock implementation of the `INavigationService`. Maintains context to the next page to navigate to and it's parameters that can be asserted against.

```csharp
/// <summary>
/// Mock service for the INavigationService dependency.
/// </summary>
/// <seealso cref="Prism.Navigation.INavigationService" />
public class NavigationServiceMock : INavigationService
{
    /// <summary>
    /// Gets the name of the page from the last navigation.
    /// </summary>
    public string PageName { get; private set; }

    /// <summary>
    /// Gets the current navigation parameters from the last navigation.
    /// </summary>
    public NavigationParameters Parameters { get; private set; }

    /// <summary>
    /// Navigates to the most recent entry in the back navigation history by popping the calling Page off the navigation stack.
    /// </summary>
    /// <param name="parameters">The navigation parameters</param>
    /// <param name="useModalNavigation">If <c>true</c> uses PopModalAsync, if <c>false</c> uses PopAsync</param>
    /// <param name="animated">If <c>true</c> the transition is animated, if <c>false</c> there is no animation on transition.</param>
    /// <returns>Whether or not the navigation navigated back.</returns>
    /// <exception cref="NotImplementedException">Not implemented.</exception>
    public Task<bool> GoBackAsync(NavigationParameters parameters = null, bool? useModalNavigation = default(bool?), bool animated = true)
    {
        throw new NotImplementedException();
    }

    /// <summary>
    /// Initiates navigation to the target specified by the <paramref name="uri" />.
    /// </summary>
    /// <param name="uri">The URI.</param>
    /// <param name="parameters">The parameters.</param>
    /// <param name="useModalNavigation">The use modal navigation.</param>
    /// <param name="animated">if set to <c>true</c> [animated].</param>
    /// <returns>An awaitable task.</returns>
    public Task NavigateAsync(Uri uri, NavigationParameters parameters = null, bool? useModalNavigation = default(bool?), bool animated = true)
    {
        this.PageName = uri.ToString();
        this.Parameters = parameters;

        return Task.FromResult(0);
    }

    /// <summary>
    /// Initiates navigation to the target specified by the <paramref name="name" />.
    /// </summary>
    /// <param name="name">The name of the target to navigate to.</param>
    /// <param name="parameters">The navigation parameters</param>
    /// <param name="useModalNavigation">If <c>true</c> uses PopModalAsync, if <c>false</c> uses PopAsync</param>
    /// <param name="animated">If <c>true</c> the transition is animated, if <c>false</c> there is no animation on transition.</param>
    /// <returns>An awaitable task.</returns>
    public Task NavigateAsync(string name, NavigationParameters parameters = null, bool? useModalNavigation = default(bool?), bool animated = true)
    {
        this.PageName = name;
        this.Parameters = parameters;

        return Task.FromResult(0);
    }
}
```
