# Welcome to the oxd Documentation

# Introduction

oxd is a mediator: it provides API's that can be called by a web application that are easier
than directly calling the API's of an OpenID Connect provider. oxd is not a proxy--in some 
cases oxd returns URL's for the OP to which the web application must redirect the person. 
To simplify the interface to developers, oxd externalizes the OpenID Connect client code. 
This is particularly useful because it enables updates to the OAuth2 client code, while keeping
the application interface the same.

![image](https://raw.githubusercontent.com/GluuFederation/docs-oxd/master/sources/img/Overview.jpg)

# License

oxd is [commercial software]((https://github.com/GluuFederation/oxd/blob/master/LICENSE)). 
Gluu offers a free version, which is limited 
to two API calls per second. Learn more about the difference between each version or
purchase a license on the [oxd webpage](https://oxd.gluu.org/#oxd-pro). 
