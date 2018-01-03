# Appium & Mobile UI Testing

## Local Installation

Follow the [Getting Started](https://appium.io/docs/en/about-appium/getting-started/?lang=en) guide to install the necessary components. Be sure to run through the installation guide for the drivers on both iOS and Android. 

It is helpful to also install [Appium Desktop](https://github.com/appium/appium-desktop/releases) to manually run a server and inspect the current session.

Use [appium-doctor](https://github.com/appium/appium-doctor) after installation of Appium and the drivers to verify the required components are installed correctly.

### Troubleshooting

To resolve issues with installing and linking Node and/or Carthage on macOS High Sierra:
* `chown` the brew directories: `sudo chown -R $(whoami) $(brew --prefix)/*` (https://github.com/Homebrew/brew/issues/3228)
* Run `brew link {your_package}`. Some directories might need to be created via `sudo mkdir {your_directory}` and then `chown` the brew directories again.

### iOS Driver

iOS uses the [XCUITest Driver](https://appium.io/docs/en/drivers/ios-xcuitest/index.html). Simply installing it allows for running tests on the iOS Simulator.

To run tests on a physical iOS device follow the [XCUITest Guide](https://appium.io/docs/en/drivers/ios-xcuitest-real-devices/). It states that you must have a provisioning profile installed that includes the device to be tested on. Once the profile is installed, you can test an `.ipa` file on a physical device using the following capabilities as stated in the above guides:

* `xcodeOrgId` - the unique team id that can be found at developer.apple.com/account in the "Membership" section
* `xcodeSigningId` - most likely "iPhone Developer"
* `app` - path to the `.ipa` file
* `udid`- UDID of the physical device, use iTunes to find this

### Android Driver

## Cloud Testing

### Sauce Labs & Test Object

## Best Practices When Writing Apps

To make writing tests easier, it is helpful to include a unique `accessibilityId` on elements that are to be interacted with (buttons, text entries, clickable areas, etc.) This allows the elements to be found by using that id.

Examples:

Xamarin - use the `AutomationId` property available on all views

```xml
<Entry AutomationId="entryToFind" ... />
<Button AutomationId="buttonToFind" ... />
<StackLayout AutomationId="viewToFind" ... />
```

TODO: Swift

TODO: Java/Kotlin

## Writing and Running Tests

Tests can be written and ran using NUnit and the [appium-dotnet-driver](https://github.com/appium/appium-dotnet-driver) client. This allows for a familiar experience in the .NET environment when writing and running the tests.

For Xamarin, a new test project can be added to the solution. For native apps, a new solution can be created with simply a UI Testing project.

First define the capabilities for which your tests will run against. Some examples:

```csharp
// iOS Simulator capabilities
iOSSimulatorCapabilities.SetCapability(MobileCapabilityType.AutomationName, "XCUITest");
iOSSimulatorCapabilities.SetCapability(MobileCapabilityType.PlatformName, "iOS");
iOSSimulatorCapabilities.SetCapability(MobileCapabilityType.DeviceName, "iPhone Simulator");
iOSSimulatorCapabilities.SetCapability(MobileCapabilityType.App, "path_to_my_app_file");

// Physical iOS device
iOSDeviceCapabilities.SetCapability(MobileCapabilityType.AutomationName, "XCUITest");
iOSDeviceCapabilities.SetCapability(MobileCapabilityType.PlatformName, "iOS");
iOSDeviceCapabilities.SetCapability(MobileCapabilityType.DeviceName, "iPhone 7 Plus");
iOSDeviceCapabilities.SetCapability(MobileCapabilityType.App, "path_to_your_ipa_file");
iOSDeviceCapabilities.SetCapability(MobileCapabilityType.Udid, "udid_of_your_device");
iOSDeviceCapabilities.SetCapability("xcodeOrgId", "your_apple_developer_team_id");
iOSDeviceCapabilities.SetCapability("xcodeSigningId", "iPhone Developer");
```

Then use those capabilities to create a driver for the respected platform:

```csharp
var androidDriver = new AndroidDriver<IWebElement>(serviceUrl, capabilities);
var iOSDriver = new IOSDriver<IWebElement>(serviceUrl, capabilities);
```

The `serviceUrl` above can either be a local instance or reference to a cloud testing platform:

```csharp
var localServiceUrl = "http://127.0.0.1:4723/wd/hub";
var sauceLabsUrl = "https://us1.appium.testobject.com/wd/hub";
```

Define a test via NUnit using the built driver:

```csharp
[TestFixture]
public class AwesomeTests
{
    private IOSDriver driver;

    [TestFixtureSetUp]
    public void BeforeAll()
    {
        // Build the driver before the start of the tests
        this.driver = new IOSDriver<IWebElement>(serviceUrl, capabilities);
    }

    [TearDown]
    public void AfterEach()
    {
        // Kill the driver after each test so that each are ran with an independent driver instance
        this.driver?.Quit();
        this.driver?.Dispose();
        this.driver = null;
    }

    [Test]
    public void EntryShouldBeAwesome()
    {
        string expectedValue = "This is awesome";
        var element = this.driver.FindElementByAccessibilityId("entryToFind");

        element.Clear();
        element.SendKeys(expectedValue);

        this.driver.HideKeyboard();

        Assert.AreEqual(expectedValue, element.Text);
    }
}
```

Once you defined the capabilities, built the driver, and created some tests, it can be then used to connect to the Appium service and run the tests by simply running the tests as normal with NUnit.
