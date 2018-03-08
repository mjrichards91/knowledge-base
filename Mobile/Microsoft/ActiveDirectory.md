# Active Directory

Guide for integrating Active Directory into a mobile app.

**It is generally recommended to perform any Active Directory authentication on the server rather then the client side. So far, this guide goes into how to do it on the client side.**

## Active Directory Authentication
In Azure, you must register your app to give it the sufficient permissions.

When asked for the tenant ID for your Azure instance, it is typically in the format `yourcompany.onmicrosoft.com`.

To be able to sign in via Active Directory, the "Windows Azure Active Directory" API and "Sign in and read user profile" permission should be added. To be able to use Microsoft's Graph API, a new permissions must be added for that API. You must click the "Grant Permissions" button when managing the permissions within Azure to finalize any changes made.

Links:

* [Authentication Scenarios](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios)
* [Microsoft Graph API Reference](https://msdn.microsoft.com/en-us/library/azure/ad/graph/api/api-catalog)


### Xamarin

There is an [MSAL framework](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) that is available and is (at the time of this writing) in preview. That library seems to be the preferred one moving forward as it hits the v2.0 endpoint. However, current experience is with the [Microsoft ADAL framework](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet).

The redirect URI to set in your app and in Azure can be anyhing in a valid URI format. Something like `https://your-authentication-app"`.

Links:

* [Quickstart](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-devquickstarts-xamarin)

### iOS

There is an [MSAL framework](https://github.com/AzureAD/microsoft-authentication-library-for-objc) that is available and is (at the time of this writing) in preview. That library seems to be the preferred one moving forward as it hits the v2.0 endpoint. Current experience is with the MSAL library.

The redirect URI to set in your app and in Azure must match what you have defined in your Info.plist file. 

```
msal[your-application-id]://auth
```

Links:

* [Quickstart](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-devquickstarts-ios)
* [v2.0 Endpoint Overview](https://docs.microsoft.com/en-us/azure/active-directory/develop/guidedsetups/active-directory-ios)
* [iOS Authentication Library](https://github.com/AzureAD/microsoft-authentication-library-for-objc)
