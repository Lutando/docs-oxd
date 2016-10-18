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

#### Get Tokens by Code

The following are the required information for Getting Tokens by Code: 

- *OxdHost* - Oxd Server's Host address
- *OxdPort* - Oxd Server's Port number
- *OxdId* - The _OXD ID_ of registered site
- *Code* - The Code from OP redirect url
- *State* - The State from OP redirect url

> **Note:** Before using this Get Tokens by Code API, you must obtain the Code and State values by authenticating the user using AuthorizationRedirectUri.

The following code snippet can be used to Get Tokens by Code.

```csharp
[HttpPost]
public ActionResult GetTokensByCode(OxdModel oxdModel)
{
	//prepare input params for Getting Tokens from a site
    var getTokenByCodeInputParams = new GetTokensByCodeParams();
    getTokenByCodeInputParams.OxdId = oxdModel.OxdId;
    getTokenByCodeInputParams.Code = oxdModel.AuthCode;
    getTokenByCodeInputParams.State = oxdModel.AuthState;

    //Get Tokens by Code
    var getTokenByCodeClient = new GetTokensByCodeClient();
    var getTokensByCodeResponse = getTokenByCodeClient.GetTokensByCode(oxdModel.OxdHost, oxdModel.OxdPort, getTokenByCodeInputParams);

    //Process response
    return Json(new { accessToken = getTokensByCodeResponse.Data.AccessToken, refreshToken = getTokensByCodeResponse.Data.RefreshToken });
}
```

#### Get User Info

The following are the required information for Getting User Info: 

- *OxdHost* - Oxd Server's Host address
- *OxdPort* - Oxd Server's Port number
- *OxdId* - The _OXD ID_ of registered site
- *AccessToken* - The _Access Token_ of the authenticated user

The following code snippet can be used to Get User Info.

```csharp
[HttpPost]
public ActionResult GetUserInfo(OxdModel oxdModel)
{
	//prepare input params for Getting User Info from a site
    var getUserInfoInputParams = new GetUserInfoParams();
    getUserInfoInputParams.OxdId = oxdModel.OxdId;
    getUserInfoInputParams.AccessToken = oxdModel.AccessToken;

    //Get User Info
    var getUserInfoClient = new GetUserInfoClient();
    var getUserInfoResponse = getUserInfoClient.GetUserInfo(oxdModel.OxdHost, oxdModel.OxdPort, getUserInfoInputParams);

    //Process response
    var userName = getUserInfoResponse.Data.UserClaims.Name.First();
    var userEmail = getUserInfoResponse.Data.UserClaims.Email == null ? string.Empty : getUserInfoResponse.Data.UserClaims.Email.FirstOrDefault();

    return Json(new { userName = userName });
}
```