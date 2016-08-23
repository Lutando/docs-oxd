# oxd-python
oxd Python is a client library for the Gluu oxd Server. 

## Deployment

### Prerequisites

* Python 2.7
* Gluu oxd Server - [Installation docs](https://www.gluu.org/docs-oxd/oxdserver/install/)

### Installation
* Download the [oxd Python Library 2.4.4](https://github.com/GluuFederation/oxd-python/releases/tag/v2.4.4) and unzip to your location of choice

```
cd oxdpython-version
python setup.py install
```

* OPTIONAL - Check code via unit tests using Nose.
```
pip install nose
nosetests
```

### Next Steps

* Scroll [below](#using-the-library-in-your-website) to learn how to use the library in an application.
* See the [API docs](https://oxd.gluu.org/api-docs/oxd-python/2.4.4) for in-depth information about the various functions and their parameters.
* See the code of a [sample Flask app](https://github.com/GluuFederation/oxd-python/blob/master/demosite) built using oxd-python.
* Browse the source code is hosted in Github [here](https://github.com/GluuFederation/oxd-python).

### Using the Library in your website

#### Configure the site

This library uses a configuration file to specify information needed 
by OpenID Connect dynamic client registration, and to save information 
that is returned, like the client id. So the config file needs to be 
*writable*. Use the 
[sample.cfg](https://github.com/GluuFederation/oxd-python/blob/master/sample.cfg) 
file as a template. 

#### Website Registration

The `Client` class of the library provides all the required methods 
required for the website to communicate with the oxd RP through sockets.

```python
from oxdpython import Client

config = "/var/www/demosite/demosite.cfg"  # This should be writable by the server
client = Client(config)
client.register_site()
```

**Note:** `register_site()` can be skipped as any `get_authorization_url()` 
automatically registers the site.

#### Get Authorization URL

Next generate an authorization url which the web application will 
redirect the person to authorize the release of personal data 
to your application from the OP.

```python
auth_url = client.get_authorization_url()
```

#### Get Tokens

After authentication and authorization at the OP, the response will 
contain code and state values. You'll need these in this method
to obtain an `id_token`, `access_token`, and `refresh_token`. 

```python
# code, scopes, state = parse_callback_url_querystring()  # Refer your web framework
tokens = client.get_tokens_by_code(code, scopes, state)
```

#### Get User Claims

User claims (information about the person) is made available by the OP 
can be fetched using the access token obtained above. Simply obtaining
tokens is not good enough--you need the user claims to know who is the 
person

```python
user = oxc.get_user_info(tokens.access_token)

# The claims can be accessed using the dot notation.
print user.username
print user.website

print user._fields  # to print all the fields

# to check for a particular field and get the information
if 'website' in user._fields:
    print getattr(user, 'website')
    # or
    print user.website
```

#### Logout the user

```python
logout_uri = oxc.get_logout_uri()
```
Redirect the user to this uri from your web application to logout the 
user.
