oxd-node
========

oxd-node is a client library for the Gluu oxd Server. 

Installation
------------

oxd-node can be install using following command:

```sh
$ npm install oxd-node
```

#### Configure the site

The [request_param.js](https://github.com/GluuFederation/oxd-node/blob/master/oxd-node/model/request_param.js) 
file contains the initial configuration and other data returned
from OpenID Connect client registration. The config file 
needs to be in a location that is *writable* by the web server. In 
general, the only two things that are required are the oxd port number 
and the redirect_uri of your application. Other values are taken
from `oxd-default-site-config.json.`

How to use
-----------

All API methods implement the [oxd Protocol](../.././oxdserver/index.md).

#### 1) register_site

```js
var oxd = require("oxd-node");
oxd.request.op_host = "public address of the site";
oxd.Request.authorization_redirect_uri= "public address of the site";
oxd.register_site(oxd.Request,function(response){
});
```

#### 2) update_site_registrations

```js
var oxd = require("oxd-node");
oxd.Request.oxd_id = "your site id";
oxd.Request.authorization_redirect_uri= "public address of the site";
oxd.update_site_registration(oxd.Request,function(response){
});
```

#### 3) get_authorization_url

```js
var oxd = require("oxd-node");
oxd.Request.oxd_id = "your site id";
oxd.Request.acr_values = ["basic"]; //optional, may be skipped (default: basic)
oxd.get_authorization_url(oxd.Request,function(response){
});
```

#### 4) get_tokens_by_code

```js
var oxd = require("oxd-node");
oxd.Request.oxd_id = "your site id";
oxd.Request.code = "code from OP redirect url";
oxd.request.scopes=[""];
oxd.get_tokens_by_code(oxd.Request,function(response){
});
```

#### 5) get_user_info

```js
var oxd = require("oxd-node");
oxd.Request.oxd_id = "your site id";
oxd.Request.access_token = "access_token from OP redirect url";
oxd.get_user_info(oxd.Request,function(response){
});
```

#### 6) get_logout_uri

```js
var oxd = require("oxd-node");
oxd.Request.oxd_id = "your site id";
oxd.get_logout_uri(oxd.Request,function(response){
});
```

