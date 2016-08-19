# Welcome to the oxd Documentation

# Introduction

oxd is a mediator, a service demon that listens on localhost, providing 
easy APIs that can be called by a web application to simplify calling 
an external OAuth2 server for authentication or authorization. oxd is 
not a proxy--sometimes it makes API calls on behalf of an application, 
but other times it just forms the right URLs and returns them to the 
application.  One advantage of using oxd over a native client library is 
that it consolidates the OAuth2 code in one package. So if there are 
updates to the OAuth2 client code, you can update the oxd-server package, 
without changing the interface to the application.

![image](https://raw.githubusercontent.com/GluuFederation/docs-oxd/master/sources/img/Overview.jpg)

# License

oxd is 
[commercial software]((https://github.com/GluuFederation/oxd/blob/master/LICENSE)).
A license is needed for each oxd server. To purchase licenses, visit the  
[oxd webpage](https://oxd.gluu.org/#oxd-pro).

