# Active Directory

Guide for integrating Active Directory into a mobile app.

## General

General guidelines for integrating into any mobile platform.

In Azure, you must register your app to give it the sufficient permissions.

When asked for the tenant ID for your Azure instance, it is typically in the format `yourcompany.onmicrosoft.com`.

To be able to sign in via Active Directory, the "Windows Azure Active Directory" API and "Sign in and read user profile" permission should be added. To be able to use Microsoft's Graph API, a new permissions must be added for that API. You must click the "Grant Permissions" button when managing the permissions within Azure to finalize any changes made.

Links:

* [Authentication Scenarios](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios)
* [Microsoft Graph API Reference](https://msdn.microsoft.com/en-us/library/azure/ad/graph/api/api-catalog)


## Xamarin

The redirect URI to set in your app and in Azure can be anyhing in a valid URI format. Something like `https://your-authentication-app"`.

Links

* [Quickstart](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-devquickstarts-xamarin)

## iOS

The redirect URI to set in your app and in Azure must match what you have defined in your Info.plist file. 

```
msal[your-application-id]://auth
```

Links:

* [Quickstart](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-devquickstarts-ios)
* [v2.0 Endpoint Overview](https://docs.microsoft.com/en-us/azure/active-directory/develop/guidedsetups/active-directory-ios)
* [iOS Authentication Library](https://github.com/AzureAD/microsoft-authentication-library-for-objc)