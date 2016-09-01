# oxd-node

oxd-node is a client library for the Gluu oxd server. For information 
about oxd, visit <http://oxd.gluu.org>

## Installation

* [Github sources](https://github.com/GluuFederation/oxd-node)

Install oxd-node using following command:
```sh
$ npm install oxd-node
```

**Prerequisite**

1. You must have oxd server installed locally on the same server 
as your node application.
2. Your application is using SSL, i.e. `https://`


## Configuration

The configuration file is `model/request_param.js` At a minimum, you 
must specify the oxd port if you have changed it from the default value
of 8099. Other default values can be specified in this file.


```
exports.oxd_port=8099 
```

**Note:** Information obtained via OpenID Connect dynamic client
registration will be persisted in this file. For this reason,
This file must be _writable_ by the server. 

## Sample Code

### 1) register_site

**Request:**

```javascript
try {
    var oxd = require("oxd-node");
    oxd.Request.authorization_redirect_uri= "https://rp.example.com/callback";  //REQUIRED
    oxd.register_site(oxd.Request,function(response){
    });
} catch (err) {
    console.log("error:" + err);
}
```

**Response:**

```javascript
{
    "status":"ok",
    "data":{
        "oxd_id":"6F9619FF-8B86-D011-B42D-00CF4FC964FF"
    }
}
```

### 2) update_site_registration

**Request:**

```javascript
try {
    var oxd = require("oxd-node");
    oxd.Request.oxd_id = "your site id";                                       //REQUIRED
    oxd.Request.authorization_redirect_uri= "https://rp.example.com/callback"; //OPTIONAL
    oxd.update_site_registration(oxd.Request,function(response){
    });
} catch (err) {
    console.log("error:" + err);
}
```

**Response:**

```javascript
{
    "status":"ok"
}
```

### 3) get_authorization_url

**Request:**

```javascript
try {
    var oxd = require("oxd-node");
    oxd.Request.oxd_id = "your site id";                      //REQUIRED
    oxd.Request.acr_values = ["basic"];                       //OPTIONAL
    oxd.get_authorization_url(oxd.Request,function(response){
    });
} catch (err) {
    console.log("error:" + err);
}
```

**Response:**

```javascript
{
    "status":"ok",
    "data":{
        "authorization_url":"https://server.example.com/authorize?response_type=code&client_id=s6BhdRkqt3&redirect_uri=https%3A%2F%2Fclient.example.org%2Fcb&scope=openid%20profile&acr_values=duo&state=af0ifjsldkj&nonce=n-0S6_WzA2Mj"
    }
}
```

**Note:** After redirecting to the above URL, the OpenID Provider will 
return a response that looks like this to the URL your application 
registered as the redirect URI (parse out the code and state):

```
HTTP/1.1 302 Found
Location: https://client.example.org/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=af0ifjsldkj&scopes=openid%20profile
```

### 4) get_tokens_by_code

**Request:**

```javascript
try {
    var oxd = require("oxd-node");                                       
    oxd.Request.oxd_id = "your site id";                      //REQUIRED
    oxd.Request.code = "code from OP redirect url";           //REQUIRED
    oxd.request.state="state from OP redirect url";           //RECOMMENDED
    oxd.get_tokens_by_code(oxd.Request,function(response){
    });
} catch (err) {
    console.log("error:" + err);
}
```

**Response:**

```javascript
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

### 5) get_user_info

**Request:**

```javascript
try {
    var oxd = require("oxd-node");                             
    oxd.Request.oxd_id = "your site id";                                 //REQUIRED
    oxd.Request.access_token = "access_token from OP redirect url";      //REQUIRED
    oxd.get_user_info(oxd.Request,function(response){
    });
} catch (err) {
    console.log("error:" + err);
}
```

**Response:**

```javascript
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

### 6) get_logout_uri

**Request:**

```javascript
try {
    var oxd = require("oxd-node");
    oxd.Request.oxd_id = "your site id";                                 //REQUIRED
    oxd.get_logout_uri(oxd.Request,function(response){                  
    });
} catch (err) {
    console.log("error:" + err);
}
```

**Response:**

```javascript
{
    "status":"ok",
    "data":{
        "uri":"https://<server>/end_session?id_token_hint=<id token>&state=<state>&post_logout_redirect_uri=<...>"
    }
}
```
