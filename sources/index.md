# Welcome to the oxd Documentation

# Introduction

oxd is a mediator: it provides easy API's that can be called by a web application to use OAuth2
profiles for authentication and authorization. oxd is not a proxy--sometimes it acts on 
behalf of an applicatoin, but others it just forms URLs and returns them to the application. 
One advantage of using oxd over a native client library is that it consolidates the OAuth2
code in one service. So if there are updates to the OAuth2 client code, you can update 
oxd without impacting the applications. 

![image](https://raw.githubusercontent.com/GluuFederation/docs-oxd/master/sources/img/Overview.jpg)

# License

oxd is [commercial software]((https://github.com/GluuFederation/oxd/blob/master/LICENSE)). 
Gluu offers a free version, which is limited 
to two API calls per second. Learn more about the difference between each version or
purchase a license on the [oxd webpage](https://oxd.gluu.org/#oxd-pro). 
