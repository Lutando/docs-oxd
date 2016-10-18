# oxd-csharp

oxd-Csharp is a C# .Net library (DLL) to interact with Gluu's OXD Server. For information about oxD, visit [http://oxd.gluu.org](http://oxd.gluu.org)

## Installation

### Prerequisites

* Visual Studio 2015
* Gluu oxD Server - [Installation docs](https://oxd.gluu.org/docs/install/)

### Library

* *Official Gluu's Nuget Package* - Install using the Visual Studio Nuget package manager console from the Gluu's official Nuget Package. Click [here](https://www.nuget.org/packages/Gluu.Oxd.OxdCSharp/) and follow the installation steps.


## Configuration

The minimal configuration required to get oxd-csharp working:

```
[oxd]
host = 127.0.0.1 //IP represents localhost
port = 8099

[client]
authorization_redirect_uri=https://your.site.org/callback
```

All the required and optional configuration items are with application developer. The oxd-csharp library does not have any specific configuration items itself.

## Using the oxd-csharp Library in your website

#### Register Site

The following are the required information for registering a Site: 

- *OxdHost* - Oxd Server's Host address
- *OxdPort* - Oxd Server's Port number
- *AuthorizationRedirectUri* - A URL which the OP is authorized to redirect the user after authorization.

The following code snippet can be used to register a site.

```csharp
[HttpPost]
public ActionResult RegisterSite(OxdModel oxdModel)
{
	//prepare input params for Register Site
    var registerSiteInputParams = new RegisterSiteParams();
    registerSiteInputParams.AuthorizationRedirectUri = oxdModel.RedirectUrl;
    registerSiteInputParams.OpHost = "https://scim-test.gluu.org";
    registerSiteInputParams.ClientName = "OxdTestingClient";

    //Register Site
    var registerSiteClient = new RegisterSiteClient();
    var registerSiteResponse = registerSiteClient.RegisterSite(oxdModel.OxdHost, oxdModel.OxdPort, registerSiteInputParams);

    //Process the response
    return Json(new { oxdId = registerSiteResponse.Data.OxdId });
}
```

#### Get Authorization URL

The following are the required information for Getting Authorization URL: 

- *OxdHost* - Oxd Server's Host address
- *OxdPort* - Oxd Server's Port number
- *OxdId* - The _OXD ID_ of registered site

The following code snippet can be used to Get Authorization URL.

```csharp
[HttpPost]
public ActionResult GetAuthorizationUrl(OxdModel oxdModel)
{
	//prepare input params for Getting Auth URL from a site
    var getAuthUrlInputParams = new GetAuthorizationUrlParams();
    getAuthUrlInputParams.OxdId = oxdModel.OxdId;

    //Get Auth URL
    var getAuthUrlClient = new GetAuthorizationUrlClient();
    var getAuthUrlResponse = getAuthUrlClient.GetAuthorizationURL(oxdModel.OxdHost, oxdModel.OxdPort, getAuthUrlInputParams);

    //Process Response
    return Json(new { authUrl = getAuthUrlResponse.Data.AuthorizationUrl });
}
```