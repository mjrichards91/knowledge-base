# Debugging
Information relating to running a local ASP.NET web application and debugging.

## Mac
If you are running Windows in a virtual machine via Parallels or some other guest service, you will need to make some configuration changes to allow access to that local server externally.

1. Set up VM to use a "Bridged" network connection.
2. Turn off Windows Firewall.
3. Update the `$(solutionDir)\.vs\config\applicationhost.config` file for your application to bind to all IP addresses:
```xml
<binding protocol="https" bindingInformation="*:44300:*" />
<binding protocol="http" bindingInformation="*:55560:*" />
```
4. Open Command Prompt as an Administrator on the Windows machine and allow external access to the IP address to anyone:
```
netsh http add urlacl url=https://*:44300/ user=everyone
netsh http add urlacl url=http://*:55560/ user=everyone
```
5. Restart your application.

**References:**
* https://stackoverflow.com/a/15809698/1013377
