# Configuration

oxD configuration file is located in the `conf/oxd-conf.json` file.

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
    "license_check_period_in_hours": 24,
    "public_key":"",
    "public_password":"",
    "license_password":""
}
```

* port - oxD socket port
* localhost_only - flag to restrict communication
* time_out_in_seconds - time out for oxd socket in seconds
* start_jetty - flag to force start embedded jetty and enable also HTTP communication (it will enable both socket and HTTP communication)
* jetty_port - jetty port
* use_client_authentication_for_pat - true if client authentication is required, if false than user authentication is performed which require user_id and user_secret specified during register_site command.
* use_client_authentication_for_aat - true if client authentication is required, if false than user authentication is performed which require user_id and user_secret specified during register_site command.
* trust_all_certs - true to trust all certificates, if false then trust_store_path must be specified to store with valid certificates
* trust_store_path - path to trust store
* license_server_endpoint - license server endpoint
* license_id - License ID. You can order valid license at https://oxd.gluu.org.
* license_check_period_in_hours - license check period
* public_key - public key of License ID (must be provided during License id purchase)
* public_password - public password of License ID (must be provided during License id purchase)
* license_password - license password of License ID (must be provided during License id purchase)

