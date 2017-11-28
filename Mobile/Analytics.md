# Analytics

## Visual Studio App Center

Pros:

1. Easy to integrate with easy, clear documentation for various platforms (Xamarin, Native, React)
1. Brand spankin' new and Microsoft owned
1. Free for most functionality
1. Analytics data:
    1. Number of active users over various spans
    1. User engagement (time per session)
    1. Device and OS information
    1. Country and language provided by carrier and OS language
    1. Distribution amongst versions
1. Continuous export of analytics into Azure
    1. Integrate into Azure Application Insights
    1. Export to PowerBI or Excel
1. Crash reporting
1. Automated UI testing via Appium on REAL devices
1. Automated builds
    1. Pre/post build scripts (i.e run unit tests)
1. App Distribution
1. Push Notifications

Cons:

1. De-obfuscated stack traces not supported in Android
1. Brand spankin' new and Microsoft owned
1. Need to manually upload .dsym file to get stack trace in iOS

## Google Firebase

Pros:

1. Backed by Google
1. Analytics data:
    1. Up to 500 distinct events
1. Many more comprehensive options to choose from:
    1. Authentication
    1. Database without a server
    1. Storage without a server
    1. Functions without a server
    1. Crash reporting via Crashlytics
    1. Performance benchmarking
    1. Predictions (predicts users likely to engage in a specific event and target them)
    1. Push notifications
    1. Remote Config (customize app behavior via server-side configuration)
    1. Indexing to get app into Google Search

Cons:

1. Harder to find documentation with Xamarin, but it exists
1. No support for Xamarin.Forms
    1. Logging would have to be done via DependencyService
1. Unable to get working as a proof of concept
