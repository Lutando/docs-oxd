# Welcome to the oxd Documentation

# Introduction

oxd is a mediator: it a service demon that listens on localhost, providing easy APIs that can be
called by a web application to simplify calling external an OAuth2 server for authentication
or authorization. oxd is not a proxy--sometimes it makes API calls on behalf of an application, but
other times it just forms the right URLs and returns them to the application.  One advantage of
using oxd over a native client library is that it consolidates the OAuth2 code in one package. So
if there are updates to the OAuth2 client code, you can update the oxd-serve package,
thus updating the security of the applications without updating them.

![image](https://raw.githubusercontent.com/GluuFederation/docs-oxd/master/sources/img/Overview.jpg)

# License

oxd is [commercial software]((https://github.com/GluuFederation/oxd/blob/master/LICENSE)).
Gluu offers a free version, which is limited
to two API calls per second. Learn more about the difference between each version or
purchase a license on the [oxd webpage](https://oxd.gluu.org/#oxd-pro).

