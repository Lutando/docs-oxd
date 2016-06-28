oxD-node
========

oxD-node is **oxD server** client, which implemented in node.js. Using it you can integrate oxD server in your Node.js application.

Installation
------------

Note : **Gluu server** and **oxD-server** needs to be installed in the hosting server to use oxD-node library with your application.

* To download and install Gluu server [click me](http://www.gluu.org/docs/).

* To download and install oxD server [click me](http://ox.gluu.org/doku.php?id=oxd:rp).

* For oxD server configuration [click me](http://ox.gluu.org/doku.php?id=oxd:home&s[]=mvn).


oxD-node can be install using following command:

```sh
$ npm install oxd-node
```

How to use
-----------

All methods of api acts according to [Protocol](../.././oxdserver/index.md).

**1) register_site**

```js
var oxd = require("oxd-node");
oxd.Request.authorization_redirect_uri= "public address of the site";
oxd.register_site(oxd.Request,function(response){
	console.log("response : "+response);
});
```

**2) update_site_registration**

```js
var oxd = require("oxd-node");
oxd.Request.oxd_id = "your site id";
oxd.Request.authorization_redirect_uri= "public address of the site";
oxd.update_site_registration(oxd.Request,function(response){
	console.log("response : "+response);
});
```

**3) get_authorization_url**

```js
var oxd = require("oxd-node");
oxd.Request.oxd_id = "your site id";
oxd.Request.acr_values = ["basic"]; //optional, may be skipped (default: basic)
oxd.get_authorization_url(oxd.Request,function(response){
	console.log("response : "+response);
});
```

**4) get_authorization_url**

```js
var oxd = require("oxd-node");
oxd.Request.oxd_id = "your site id";
oxd.Request.code = "code from OP redirect url";
oxd.get_tokens_by_code(oxd.Request,function(response){
	console.log("response : "+response);
});
```

**5) get_user_info**

```js
var oxd = require("oxd-node");
oxd.Request.oxd_id = "your site id";
oxd.Request.access_token = "access_token from OP redirect url";
oxd.get_user_info(oxd.Request,function(response){
	console.log("response : "+response);
});
```

**6) get_logout_uri**

```js
var oxd = require("oxd-node");
oxd.Request.oxd_id = "your site id";
oxd.get_logout_uri(oxd.Request,function(response){
	console.log("response : "+response);
});
```

