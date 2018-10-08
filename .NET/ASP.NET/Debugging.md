# Debugging
Information relating to running a local ASP.NET web application and debugging.

## Mac
If you are running Windows in a virtual machine via Parallels or some other guest service, you will need to make some configuration changes to allow access to that local server externally.

1. Set up VM to use a [Bridged network connection](https://kb.parallels.com/en/4948#bridged).
1. Turn off Windows Firewall.  
1. If you cannot turn off Windows Firewall, allow IIS Express through Windows firewall:

    ```
    Start -> Windows Firewall with Advanced Security -> Inbound Rules -> New Rule...
    ```
    Choose:
    * Program `%ProgramFiles%\IIS Express\iisexpress.exe` 
    * OR Port `YOUR_PORT` TCP . 
1. Update the `$(solutionDir)\.vs\config\applicationhost.config` file for your application to bind to all IP addresses:

    ```xml
    <binding protocol="https" bindingInformation="*:[your-https-port]:*" />
    <binding protocol="http" bindingInformation="*:[your-http-port]:*" />
    ```
1. Open Command Prompt as an Administrator on the Windows machine and allow external access to the IP address to anyone:

    ```
    netsh http add urlacl url=https://*:[your-https-port]/ user=everyone
    netsh http add urlacl url=http://*:[your-http-port]/ user=everyone
    ```
1. Restart your application.

**References:**
* https://stackoverflow.com/a/15809698/1013377
