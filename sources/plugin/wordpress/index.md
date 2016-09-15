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
 
In your WP admin menu panel you should now see the OpenID Connect menu tab. Click on it.

1. Membership: must be checked.
2. New User Default Role: Please choose user role. 
3. URI of the OpenID Connect Provider: Please insert URI of the OpenID Connect Provider.
4. oxd port: choose the port which is using oxd-server (see in `oxd-server/conf/oxd-conf.json` file).
5. Click next to continue.

If your OpenID Provider supports `https://OpenID-Provider/.well-known/openid-configuration` link, you can know that your provider support dynamic registration. 

1. If `registration_endpoint` parameter exists, it means that OP supports dynamic registration
2. If `end_session_endpoint` parameter exists, it means that OP supports logout from OP too.

#### If your OpenID Connect Provider supports dynamic registration you will see bottom page.

![General](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/1.png) 

#### If your OpenID Connect Provider doesn't support dynamic registration you need to insert your OpenID Provider client_id and client_secret.

#### For creating client_id and client_secret use redirect uri `https://{site-base-url}/index.php?option=oxdOpenId`.

![General](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/2.png) 

#### If you have successfully registered your OpenID Connect Provider, which support dynamic registration, you will see bottom page.

If you use Gluu server as OpenID Provider, to make sure everything is configured properly, login to your Gluu Server and navigate to the OpenID Connect > Clients page. Search for your `oxd id`.

![oxd_id](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/4.png) 

#### If you have successfully registered your OpenID Connect Provider, which doesn't supports dynamic registration, you will see bottom page.

![oxd_id](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/3.png) 

### OpenID Connect Configuration

#### Scopes

If your OpenID Provider supports `https://OpenID-Provider/.well-known/openid-configuration` link, you can find your supported scopes.

Scopes are groups of user attributes that are sent from your OP to the application during login and enrollment. 

If you use Gluu server as OpenID Provider, you can view all available scopes in your Gluu Server by navigating to the OpenID Connect > Scopes intefrace. 

In the Plugin interface you can enable, disable and delete scopes. 

![Scopes2](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/5.png) 

#### Manage Authentication

To signal which type of authentication should be used, an OpenID Connect client may request a specific authentication context class reference value or "acr". 

##### Send user straight to OpenID Provider for authentication

1. If checkbox checked your site users on clicking `Login` button will go to authentication for logging.

##### Select acr

If your OpenID Provider support `https://OpenID-Provider/.well-known/openid-configuration` link, you can find your supported acr_values and in `Select acr` section and choose that mechanism, which you want for authentication. 

1. If `Select acr` selected on `none`, it will login your users to site by your OpenID Provider default authentication type.


##### Add acr

In `Add acr` you can add your OpenID Provider available acr_values and choose in section `Select acr` for authentication.

