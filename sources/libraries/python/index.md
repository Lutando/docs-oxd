# oxd-python
Python Client Library for the [Gluu oxD](https://www.gluu.org/docs-oxd/).

**oxdpython** is a thin wrapper around the [communication protocol](https://www.gluu.org/docs-oxd/oxdserver/) of oxD server. This can be used to access the OpenID connect & UMA Authorization end points of the Gluu Server via the oxD RP. This library provides the function calls required by a website to access user information from a OpenID Connect Provider (OP) by using the OxD as the Relying Party (RP).

## Using the Python Library to build your website

### Prerequisites

* Install `gluu-oxd-server`

### Configuring

Create a copy of the [sample configuration](https://github.com/GluuFederation/oxd-python/blob/master/sample.cfg) file for your website in a server *writable* location. When the website is registered with the OP, its ID and other peristant information about the website are stored in this config file. So the config file needs to be *writable* for the server. The `sample.cfg` file contains complete documentation about itself.

### Importing

The `Client` class of the library provides all the required methods required for the website to communicate with the oxD RP through sockets.

```python
from oxdpython import Client

config = "/var/www/demosite/demosite.cfg"  # NOTE: This should be writable by the server
client = Client(config)
```

### Website Registration

The website can be registered with the OP using the `client.register_client()` call. This can be skipped as every call to `get_authorization_url()` registers the site if not already registered.

### Get Authorization URL

The first step is to generate an authorization url which the user can visit to authorize your application to use the information from the OP.

```python
auth_url = client.get_authorization_url()
```
Using the above url the website can redirect the user for authentication can authorization at the OP.

### Get access token

The website needs to parse the information fromt the callback url and pass it on to get the access token for fetching user information.

```python
token = client.get_tokens_by_code(code, scopes, state)
```
The values for code, scope and state are parsed from the callback url querystring. Refer to your web framework to how to get these values from the url.

### Get user claims

Claims (information fields) made availble by the OP can be fethed using the access token obtained above.

```python
user = oxc.get_user_info(token)
```

### Using the claims

The claims can be accessed using the dot notation.
```python
print user.username
print user.inum
print user.website
```
The availability of various claims are completely dependent on the OP. Listing the fields of user can give list of all the available claims.

```python
print user._fields  # to print all the fields

# to check for a particular field and get the information
if 'website' in user._fields:
    print getattr(user, 'website')  # or
    print user.website
```

