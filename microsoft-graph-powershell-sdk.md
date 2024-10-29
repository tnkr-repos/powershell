# MICROSOFT GRAPH POWERSHELL SDK

- What is Microsoft Graph PowerShell SDK?
    - API that wraps around the Microsoft Graph APIs
    - Contains PowerShell commands for automation at scale using Graph APIs
    - Allows connecting to Microsoft 365 and Azure Active Directory services

- What are the features?
  - Provides access to all the Microsoft Graph APIs
    - Connects all the Microsoft 365 services together into a single RESTful
    endpoint
    - Includes Microsoft 365 services like Azure Entra ID, Sharepoint Online,
    Exchange Online, Microsoft Teams. You'll call them with specific endpoints
    around objects instead such as users and groups
    - Accessed using a single access token and endpoint (instead of accessing
    multiple endpoints, one for each service)
    - Azure AD Graph PowerShell is based on Azure AD Graph (**DEPRECATED**)
  - Support for modern authentication (MFA)
    - Supports Microsoft Authentication Library (MSAL) which is better than
    Azure Active Directory Authentication Library (ADAL) as it works across
    services, and it supports username/password, multifactor and certificate
    authentication

- What are the Microsoft Graph API versions?
  - Published
  - Beta - latest features are present
  - We can use either version when utilizing the PowerShell commands

```powershell
Get-MgProfile # get current API endpoint version
Select-MgProfile -Name "beta" # set the api to the beta endpoint
Select-MgProfile -Name "v1.0" # set the api to the v1.0 endpoint
```

- What are the categories of Graph PowerShell SDK?
  - Azure Active Directory Applications (App registrations, enterprise apps)
  - Devices (Mobile, Windows, Mac)
  - Calendar (Part of Microsoft Exchange)
  - Bookings
  - Groups (Microsoft 365 groups to Security Groups in Azure Entra ID)
  - Files (Part of SharePoint Online, Onedrive for Business)
  - Identity
  - Reports
  - Planner
  - Mail (from Exchange Online)
  - Security 
  - Search
  - Sites
  - Users and People

- What is the workflow like?
  - There are a lot of categories we can access, but we don't need to know the
  service they belong to because the Microsoft Graph makes an object available
  to us, and the PowerShell SDK makes the same object available to me
  - So to get information about me, we have to connect to user object, and if I
  want to see the calendar events or the mail, we can Calendar or Mail for the
  user instead of having to connect to Azure Entra ID, getting the user object,
  then connecting to Exchange Online, then Teams, etc.

- How to install Microsoft Graph PowerShell SDK?
  - NuGet provider should be installed to interact with PowerShell Gallery
  - Set the Execution Policy to `RemoteSigned`
  - There are two scopes (similar to what we face in GUI - Just for Me, or all
  users of system) - `CurrentUser` or `AllUsers`
  - A lot of submodules will also be installed while installing Graph Module -
  these submodules directly map to different categories in the Graph API

```powershell
Install-PackageProvider -Name NuGet -Force
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Install-Module Microsoft.Graph -Scope CurrentUser # or use AllUsers
Get-InstalledModule Microsoft.Graph
Update-Module Microsoft.Graph
```

- What are the naming conventions for PowerShell commands of Graph module?
  - The commands match the name of the REST API which they wrap (If the API has
  a name `AddUser` then there will be a PowerShell command called `AddUser`)
  - They follow the Verb-Noun convention
  - Complex commands are implemented as OData functions (usually with `Invoke`
  verb which allow us to pass objects to them)
  - "GET", "POST", "PUT", "PATCH", "DELETE" - map to their REST API equivalents

0