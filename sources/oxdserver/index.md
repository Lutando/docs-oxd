# oxd server overview

oxd makes it super simple to authenticate a person with OpenID Connect, to 
protect web resources with OAuth2, or to write a client that calls an OAuth2
protected API. 

The oxd Server is designed to work as standalone application (without Web Application Container, 
like tomcat). It's a mediator--providing API's that make it easier for 
developers to use OAuth2 protocols. By default, it is restricted to `localhost`--so
the oxd server should be installed on each server that has web applications. But stay
tuned, Gluu is introducing a gateway that will enable a centralized deployment
of an oxd server. 
 
oxd API's can be called with any platform that can make REST calls, but 
Gluu provides several native libraries, currently for Php, Java, Python,
node, Ruby and C#.

oxd is commercial software. There is a free version that is limited to two transactions
per second, which may be enough for many low volume sites. For more information on 
purchasing a commercial version of oxd, see the [website](http://oxd.gluu.org)

## Web site protection with oxd

Libraries provide convenient methods to the web site developer which 
for calling the oxd API's. The concrete library depends on the programming language 
used by a web site. We will use Java as an example on this page.

![oxd-overview](https://raw.githubusercontent.com/GluuFederation/docs-oxd/master/sources/img/Overview.jpg)

First of all, the web site must register itself with oxd Server via registration 
command (using java/python/php library). With registration it gets oxd_id from oxd Server. 
oxd_id must be passed to all commands.

Web site configuration:
```
   oxd_address : localhost:8090
   oxd_id : 6F9619FF-8B86-D011-B42D-00CF4FC964FF
```
oxd_id (6F9619FF-8B86-D011-B42D-00CF4FC964FF) - GUID for web site. It can be any GUID 
that does not exist yet on oxd Server.


## Overview of entire process

### OpenID Connect - Authorization Code Grant overview

```
1. Register site
2. Get authorization URL (use this to redirect person to the OP)
3. OP returns code in response
4. Call get_tokens_by_code to obtain access & id_token
5. Use access token to obtain user claims
6. Logout
```

## Library/Plugin (Python/PHP/Java)

All libraries support the following commands for OpenID Connect. Not all libraries currently
support the OAuth2 access management API's, but they will by the next release--check your 
specific library to confirm.

### Register site

During the registration operation oxd dynamically registers a client keeps it in 
its configuration.

All parameters in register_site operation are optional except `authorization_redirect_uri`.
This is the URL that the OpenID Connect Provider (OP) will send the person to after successful
authentication. 

All fallback values are taken from `oxd-default-site-config.json` If the `op_host` is missing 
from the register_site command, it must be present here. However, all other values
will be obtained via OpenID Connect discovery and dynamic client registration. 
The purpose of the properties is to enable you to override these values. 

This method returns `ox-id`. The reason for this is that several applications may share an instance 
of oxd, and this identifier is used by oxd to distinguish difference in configuration between 
them.

Request:

```json
{
    "command":"register_site",
    "params": {
        "redirect_uris": ["https://client.example.org/cb"],            <- REQUIRED
        "op_host":"https://ce-dev.gluu.org"                            <- OPTIONAL (But if missing, must be present in defaults) 
        "authorization_redirect_uri": "https://client.example.org/cb", <- OPTIONAL 
        "post_logout_redirect_uri": "https://client.example.org/cb",   <- OPTIONAL 
        "application_type":"web",                                      <- OPTIONAL 
        "response_types": ["code", "id_token", "token"]                <- OPTIONAL 
        "grant_types": ["authorization_code"]                          <- OPTIONAL 
        "scope":["openid"],                                            <- OPTIONAL 
        "acr_values":["basic"],                                        <- OPTIONAL
        "client_jwks_uri":"",                                          <- OPTIONAL
        "client_token_endpoint_auth_method":"",                        <- OPTIONAL
        "client_request_uris":[],                                      <- OPTIONAL
        "client_logout_uris":[],                                       <- OPTIONAL
        "client_sector_identifier_uri":[],                             <- OPTIONAL
        "contacts":["yuriy@gluu.org"],                                 <- OPTIONAL
        "ui_locales":[],                                               <- OPTIONAL
        "claims_locales":[],                                           <- OPTIONAL
        "client_id":"<client id of existing client>",                  <- OPTIONAL ignores all other parameters and skips new client registration forcing to use existing client (client_secret is required if this parameter is set)
        "client_secret":"<client secret of existing client>",          <- OPTIONAL must be used together with client_secret.
    }
}
```

Response:

```json
{
    "status":"ok",
    "data":{
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF"
    }
}
```

### Update site registration

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"update_site_registration",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",              <- REQUIRED
        "authorization_redirect_uri": "https://client.example.org/cb",<- OPTIONAL 
        "post_logout_redirect_uri": "https://client.example.org/cb",  <- OPTIONAL 
        "client_logout_uris":["https://client.example.org/logout"],   <- OPTIONAL
        "application_type":"web",                                     <- OPTIONAL 
        "response_type":["code"],                                     <- OPTIONAL
        "grant_types":[],                                             <- OPTIONAL
        "redirect_uris": ["https://client.example.org/cb"],           <- OPTIONAL
        "scope": ["profile"],                                         <- OPTIONAL
        "acr_values":[""],                                            <- OPTIONAL
        "client_secret_expires_at":1335205592410                      <- OPTIONAL can be used to extends client lifetime (milliseconds since 1970)
        "client_jwks_uri":"",                                         <- OPTIONAL
        "client_token_endpoint_auth_method":"",                       <- OPTIONAL
        "client_request_uris":[],                                     <- OPTIONAL
        "client_logout_uris":[],                                      <- OPTIONAL
        "client_sector_identifier_uri":"",                            <- OPTIONAL
        "contacts":["yuriy@gluu.org"]                                 <- OPTIONAL
        "ui_locales":[],                                              <- OPTIONAL
        "claims_locales":[],                                          <- OPTIONAL
    }
}
```

Response:

```json
{
    "status":"ok"
}
```


### Get authorization url

Note: authorization_code grant type



Request:

```json
{
    "command":"get_authorization_url",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",
        "acr_values":["basic", "duo"],                         <- optional, may be skipped (default: basic)
        "prompt":"login"                                       <- optional, skipped if no value specified or missed. prompt=login is required if you want to force alter current user session (in case user is already logged in from site1 and site2 construsts authorization request and want to force alter current user session)
    }
}
```

Response:

```json
{
    "status":"ok",
    "data":{
        "authorization_url":"  https://server.example.com/authorize?response_type=id_token%20token
    &client_id=s6BhdRkqt3
    &redirect_uri=https%3A%2F%2Fclient.example.org%2Fcb
    &scope=openid%20profile
    &state=af0ifjsldkj
    &nonce=n-0S6_WzA2Mj"
    }
}
```

### Get Tokens (ID & Access) by Code

Note: Library (php/python/java/node) must provide utility methods for web site to parse response 
from OP and send parsed code and state parameters to oxd:

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

```
HTTP/1.1 302 Found
Location: https://client.example.org/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=af0ifjsldkj&scopes=openid%20profile
```

Request:

```json
{
    "command":"get_tokens_by_code",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",
        "code":"I6IjIifX0",                <- Required, code from OP redirect url (see example above)
        "state":"af0ifjsldkj",             <- Optional can be skipped
        "scopes":["openid", "profile"]     <- Required, scopes from OP redirect url (see example above)
    }
}
```

Response:

```
{
    "status":"ok",
    "data":{
        "access_token":"SlAV32hkKG",
        "expires_in":3600,
        "refresh_token":"aaAV32hkKG1"
        "id_token":"eyJ0 ... NiJ9.eyJ1c ... I6IjIifX0.DeWt4Qu ... ZXso",
        "id_token_claims": {
             "iss": "https://server.example.com",
             "sub": "24400320",
             "aud": "s6BhdRkqt3",
             "nonce": "n-0S6_WzA2Mj",
             "exp": 1311281970,
             "iat": 1311280970,
             "at_hash": "MTIzNDU2Nzg5MDEyMzQ1Ng"
        }
    }
}
```

### Get User Info

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"get_user_info",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",
        "access_token":"SlAV32hkKG"
    }
}
```

Response:

```json
{
    "status":"ok",
    "data":{
        "claims":{
            "sub": ["248289761001"],
            "name": ["Jane Doe"],
            "given_name": ["Jane"],
            "family_name": ["Doe"],
            "preferred_username": ["j.doe"],
            "email": ["janedoe@example.com"],
            "picture": ["http://example.com/janedoe/me.jpg"]
        }
    }
}
```

### Log out URI

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"get_logout_uri",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",
        "id_token_hint":"eyJ0 ... NiJ9.eyJ1c ... I6IjIifX0.DeWt4Qu ... ZXso" <-- OPTIONAL (oxd server will use last used ID Token)
        "post_logout_redirect_uri":"<post logout redirect uri here>"   <-- OPTIONAL
        "state":"<site state>",                                        <-- OPTIONAL
        "session_state":"<session state>"                              <-- OPTIONAL
    }
}
```

Response:

```json
{
    "status":"ok",
    "data":{
        "uri":"https://<server>/end_session?id_token_hint=<id token>&state=<state>&post_logout_redirect_uri=<...>"
    }
}
```

## UMA

### UMA Resource Server

oxd Client Library used by Resource Server application MUST:

- Register protection document (with uma_rs_protect command)
- Intercept HTTP call (before actual REST resource call) and check whether it's allowed to proceed with call or reject it according to uma_rs_check_access command response:
    - Allow access - if response from uma_rs_check_access is "allowed" or "not_protected" error is returned.
    - uma_rs_check_access returned "denied" with ticket then return back HTTP response
```http
HTTP/1.1 401 Unauthorized
WWW-Authenticate: UMA realm="example",
      as_uri="https://as.example.com",
      ticket="016f84e8-f9b9-11e0-bd6f-0021cc6004de"
```
    - uma_rs_check_access returned "denied" without ticket then return back HTTP response

```http
HTTP/1.1 403 Forbidden
Warning: 199 - "UMA Authorization Server Unreachable"
```

### UMA RS Protect resources

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"uma_rs_protect",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",   <- REQUIRED
        "resources":[        <-  REQUIRED as parameter here we have protection json that describes resources on RS
            {
                "path":"/photo",
                "conditions":[
                    {
                        "httpMethods":["GET"],
                        "scopes":[
                            "http://photoz.example.com/dev/actions/view"
                        ]
                    },
                    {
                        "httpMethods":["PUT", "POST"],
                        "scopes":[
                            "http://photoz.example.com/dev/actions/all",
                            "http://photoz.example.com/dev/actions/add"
                        ],
                        "ticketScopes":[
                            "http://photoz.example.com/dev/actions/add"
                        ]
                    }
                ]
            },
            {
                "path":"/document",
                "conditions":[
                    {
                        "httpMethods":["GET"],
                        "scopes":[
                            "http://photoz.example.com/dev/actions/view"
                        ]
                    }
                ]
            }
        ]
    }
}
```

Response:

```json
{
    "status":"ok"
}
```

### UMA RS Check Access

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"uma_rs_check_access",
    "params": {
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",
        "rpt":"eyJ0 ... NiJ9.eyJ1c ... I6IjIifX0.DeWt4Qu ... ZXso",    <-- REQUIRED RPT or blank value if absent (not send by RP)
        "path":"<path of resource>",                                   <-- REQUIRED Path of resource (e.g. http://rs.com/phones), /phones should be passed
        "http_method":"<http method of RP request>"                    <-- REQUIRED Http method of RP request (GET, POST, PUT, DELETE)
    }
}
```

Sample of RP request:
```
GET /users/alice/album/photo HTTP/1.1
Authorization: Bearer vF9dft4qmT
Host: photoz.example.com
```

Params:
```
rpt: 'vF9dft4qmT'
path: /users/alice/album/photo
http_method: GET
```

Access Granted response:

```json
{
    "status":"ok",
    "data":{
        "access":"granted"
    }
}
```

Access Denied with ticket response:

```json
{
    "status":"ok",
    "data":{
        "access":"denied"
        "www-authenticate_header":"UMA realm=\"example\",
                                   as_uri=\"https://as.example.com\",
                                   error=\"insufficient_scope\",
                                   ticket=\"016f84e8-f9b9-11e0-bd6f-0021cc6004de\"",
        "ticket":"016f84e8-f9b9-11e0-bd6f-0021cc6004de"
    }
}
```

Access Denied without ticket response:

```json
{
    "status":"ok",
    "data":{
        "access":"denied"
    }
}
```


Errors:

Resource is not protected
```json
{
    "status":"error",
    "data":{
        "error":"invalid_request"
        "error_description":"Resource is not protected. Please protect your resource first with uma_rs_protect command."
    }
}
```

## UMA Requesting Party

### UMA RP - Get RPT

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"uma_rp_get_rpt",
    "params": {
         "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",  <- REQUIRED
         "force_new": false                                <- REQUIRED indicates whether return new RPT, in general should be false, so oxd server can cache/reuse same RPT
    }
}
```

Response:

```json
{
     "status":"ok",
     "data":{
         "rpt":"vF9dft4qmT"
     }
}
```

### UMA RP - Authorize RPT

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"uma_rp_authorize_rpt",
    "params": {
         "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",  <- REQUIRED
         "rpt": "vF9dft4qmT",                              <- REQUIRED
         "ticket": "016f84e8-f9b9-11e0-bd6f-0021cc6004de"  <- REQUIRED
    }
}
```

Authorized Response (Success):

```json
{
     "status":"ok",
}
```

Not authorized error:
```json
{
    "status":"error",
    "data":{
        "code":"not_authorized"
        "description":"RPT is not authorized."
    }
}
```


Invalid ticket error:
```json
{
    "status":"error",
    "data":{
        "code":"invalid_ticket"
        "description":"Ticket is not valid (outdated or not present on Authorization Server)."
    }
}
```

Invalid rpt error:
```json
{
    "status":"error",
    "data":{
        "code":"invalid_rpt"
        "description":"RPT is not valid (outdated or not present on Authorization Server)."
    }
}
```

### UMA RP - Get GAT

GAT stands for Gluu Access Token. It is invented by Gluu and is described here: https://ox.gluu.org/doku.php?id=uma:oauth2_access_management.

For latest and most up to date parameters of command please check latest successful [jenkins build](https://ox.gluu.org/jenkins/job/oxd)

Request:

```json
{
    "command":"uma_rp_get_gat",
    "params": {
         "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF",  <- REQUIRED
         "scopes": [                                       <- REQUIRED RP should know required scopes in advance
             "http://photoz.example.com/dev/actions/add",
             "http://photoz.example.com/dev/actions/view",
             "http://photoz.example.com/dev/actions/edit"
         ]
    }
}
```

Response:

```json
{
     "status":"ok",
     "data":{
         "gat":"fg6vF9dft4qmT"
     }
}
```

## References

- [UMA 1.0.1 Specification](https://docs.kantarainitiative.org/uma/rec-uma-core.html#permission-failure-to-client)
- [Sample RS of Java Resteasy HTTP interceptor of uma-rs](https://github.com/GluuFederation/uma-rs/blob/master/uma-rs-resteasy/src/main/java/org/xdi/oxd/rs/protect/resteasy/RptPreProcessInterceptor.java)
