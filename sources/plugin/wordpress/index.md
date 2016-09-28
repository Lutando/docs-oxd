[TOC]

# WordPress OpenID Connect Single Sign-On (SSO) Plugin By Gluu

![image](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/plugin.jpg)

Gluu's WordPress OpenID Connect Single Sign-On (SSO) Plugin will enable you to authenticate users against any standard OpenID Connect Provider (OP). If you don't already have an OP you can [deploy the free open source Gluu Server](https://gluu.org/docs/deployment).  

## Requirements
In order to use the WordPress plugin, you will need to have deployed a standard OP like the Gluu Server and the oxd Server.

* [Gluu Server Installation Guide](https://www.gluu.org/docs/deployment/).

* [oxd Server Installation Guide](https://oxd.gluu.org/docs/oxdserver/install/)


## Installation
 
### Download
[Github source](https://github.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/archive/v2.4.4.zip).

[Link to WordPress marketplace](https://wordpress.org/plugins/openid-connect-sso-by-gluu/)

### Upload
Open your WordPress site plugin page, e.g. `https://{site-base-url}/wp-admin/plugin-install.php?tab=upload`, upload the plugin and click on the install now button.

### Activate 

Activate the plugin by performing the following steps:
 
1. Go to `https://{site-base-url}/wp-admin/plugins.php`
2. Find OpenID Connect Single Sign-On (SSO) Plugin By Gluu and click the activate button.

## Configuration

### General
 
In your WP admin menu panel you should now see the OpenID Connect menu tab. Click the link to navigate to the General configuration  page:

![General](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/1.png) 

1. Membership: must be checked. 
2. New User Default Role: specify which role to give to new users upon registration.  
3. URI of the OpenID Connect Provider: insert the URI of the OpenID Connect Provider.
4. Custom URI after logout: custom URI after logout (for example "Thank you" page).
5. oxd port: enter the oxd-server port (you can find this in the `oxd-server/conf/oxd-conf.json` file).
6. Click `Register` to continue.

If your OpenID Provider supports dynamic registration, no additional steps are required in the general tab and you can navigate to the [OpenID Connect Configuration](#openid-connect-configuration) tab. 

If your OpenID Connect Provider doesn't support dynamic registration, you will need to insert your OpenID Provider `client_id` and `client_secret` on the following page.

![General](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/2.png) 

To generate your `client_id` and `client_secret` use the redirect uri: `https://{site-base-url}/index.php?option=oxdOpenId`.

> If you are using a Gluu server as your OpenID Provider, you can make sure everything is configured properly by logging into to your Gluu Server, navigate to the OpenID Connect > Clients page. Search for your `oxd id`.

### OpenID Connect Configuration

![OpenID Connect Configuration](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/5.png)

#### Scopes

Scopes are groups of user attributes that are sent from the OP to the application during login and enrollment. By default, the requested scopes are `profile`, `email`, and `openid`.  

To view your OP's available scopes, in a web browser navigate to `https://OpenID-Provider/.well-known/openid-configuration`. For example, here are the scopes you can request if you're using [Google as your OP](https://accounts.google.com/.well-known/openid-configuration). 

If you are using a Gluu server as your OpenID Provider, you can view all available scopes by navigating to the OpenID Connect > Scopes intefrace. 

In the Plugin interface you can enable, disable and delete scopes. 

#### Manage Authentication

##### Send user straight to OpenID Provider for authentication

Check this box so that when users attempt to login they are sent straight to the OP, bypassing the local WP login screen,.

##### Select acr

To signal which type of authentication should be used, an OpenID Connect client may request a specific authentication context class reference value (a.k.a. "acr"). The authentication options available will depend on which types of mechanisms the OP has been configured to support. The Gluu Server supports the following authentication mechanisms out-of-the-box: username/password (basic), Duo Security, Super Gluu, and U2F tokens, like Yubikey.  

Navigate to your OpenID Provider confiuration webpage `https://OpenID-Provider/.well-known/openid-configuration` to see supported `acr_values`. In the `Select acr` section of the plugin page, choose the mechanism which you want for authentication. 

Note: If the `Select acr` value is `none`, users will be sent to pass the OP's default authentication mechanism.

##### Add acr

The plugin will detect the OPs supported ACR values if this information is published in the OP's discovery endpoint. However, if the OP does not publish supported ACR values, you may need to add them manually. 

