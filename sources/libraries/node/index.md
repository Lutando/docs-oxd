oxD-node
========

oxD-node is **oxD server** client, which implemented in node.js. Using it you can integrate oxD server in your Node.js application.

Installation
------------

Note : **Gluu server** and **oxD-server** needs to be installed in the hosting server to use oxD-node library with your application.

* To download and install Gluu server [click me](http://www.gluu.org/docs/).

* To download and install oxD server [click me](https://www.gluu.org/docs-oxd).

* For oxD server configuration [click me](https://www.gluu.org/docs-oxd).


oxD-node can be install using following command:

```sh
$ npm install oxd-node
```

#### Configure the site

Once the library is installed, create a copy of the sample configuration file for your website in a server *writable* location and edit the configuration. For example

```
in model/request_param.js, find exports.port=null and enter port no inplace of "null" which ever is free on your server.
```

**Note:** The website is registered with the OP and its ID is stored in this config file, also are the other peristant information about the website. So the config file needs to be *writable* for the server. The [sample.cfg](https://github.com/GluuFederation/oxd-python/blob/master/sample.cfg) file contains complete documentation about itself.

How to use
-----------

All methods of api acts according to [Protocol](../.././oxdserver/index.md).

#### 1) register_site

```js
var oxd = require("oxd-node");
oxd.request.op_host = "public address of the site";
oxd.Request.authorization_redirect_uri= "public address of the site";
oxd.register_site(oxd.Request,function(response){
});
```

#### 2) update_site_registration

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

