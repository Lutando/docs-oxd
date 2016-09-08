# Configuration

oxD configuration consists of two files :

* `conf/oxd-conf.json` - general configuration
* `conf/oxd-default-site-config.json` - fallback configuration for "Register site" command, see details on 
[Protocol page](https://oxd.gluu.org/docs/oxdserver/)

## oxd-conf.json

The contents of the configuration file is as follows:

```
oxd-conf.json
{
    "port":8099,
    "localhost_only":true,
    "time_out_in_seconds":0,
    "jetty_port":8098,
    "start_jetty":false,
    "use_client_authentication_for_pat":true,
    "use_client_authentication_for_aat":true,
    "trust_all_certs":true,
    "trust_store_path":"",
    "license_server_endpoint":"",
    "license_id":"",
    "public_key":"",
    "public_password":"",
    "license_password":""
}
```

* port - oxD socket port
* localhost_only - flag to restrict communication
* time_out_in_seconds - time out for oxd socket in seconds. oxd closes sockets automatically after this time out (stops listen commands). Zero means listen indefinitely.
* start_jetty - flag to force start embedded jetty and enable also HTTP communication (it will enable both socket and HTTP communication)
* jetty_port - jetty port
* use_client_authentication_for_pat - true if client authentication is required, if false than user authentication is performed which require user_id and user_secret specified during register_site command.
* use_client_authentication_for_aat - true if client authentication is required, if false than user authentication is performed which require user_id and user_secret specified during register_site command.
* trust_all_certs - true to trust all certificates, if false then trust_store_path must be specified to store with valid certificates
* trust_store_path - path to trust store e.g `/etc/ssl/certs/cacerts`
* license_server_endpoint - `https://license.gluu.org/oxLicence`
* license_id - License ID. You can [order valid license](https://oxd.gluu.org). Without a license you are limited to 2 transactions per second.
* public_key - public key of License ID (must be provided during License id purchase)
* public_password - public password of License ID (must be provided during License id purchase)
* license_password - license password of License ID (must be provided during License id purchase)

## oxd-default-site-config.json

```json
conf/oxd-default-site-config.json
{
    "op_host":"",
    "authorization_redirect_uri":"",
    "post_logout_redirect_uri":"",
    "response_types":["code"],
    "grant_type":["authorization_code"],
    "acr_values":["basic"],
    "scope":["openid", "profile"],
    "ui_locales":["en"],
    "claims_locales":["en"],
    "client_jwks_uri":"",
    "contacts":[]
}
```

* op_host - must point to a valid [Gluu Server CE installation](http://gluu.org/docs). (Sample : "op_host":"https://idp.example.org")
* authorization_redirect_uri - URL that the OpenID Connect Provider (OP) will redirect the person to after  successful authentication
* post_logout_redirect_uri - URL to which the RP is requesting that the End-User's User Agent be redirected after a logout has been performed
* response_types - JSON array containing a list of the OAuth 2.0 response_type values that the site is declaring that it will restrict itself to using
* grant_type - JSON array containing a list of the OAuth 2.0 Grant Types that the Client is declaring that it will restrict itself to using
* acr_values - specified authentication method (basic, duo, u2f)
* scope - JSON array containing a list of the scopes that the Client is declaring that it will restrict itself to using
* ui_locales - End-User's preferred languages and scripts for the user interface, represented as a space-separated list of BCP47 [RFC5646] language tag values, ordered by preference
* claims_locales - End-User's preferred languages and scripts for Claims being returned, represented as a space-separated list of BCP47 [RFC5646] language tag values, ordered by preference
* contacts - array of e-mail addresses of people responsible for this Client
