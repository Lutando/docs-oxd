[TOC]

# WordPress OpenID Connect Single Sign On (SSO) Plugin By Gluu

![image](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/plugin.jpg)

Gluu's WordPress OpenID Connect Single Sign On (SSO) Plugin will enable you to authenticate users against any standard OpenID Connect Provider (OP). If you don't already have an OP you can [deploy the free open source Gluu Server](https://gluu.org/docs/deployment).  

## Requirements
In order to use the WordPress plugin, you will need to have deployed a standard OP like the Gluu Server and the oxd Server.

* [Gluu Server Installation Guide](https://www.gluu.org/docs/deployment/).

* [oxd Server Installation Guide](https://oxd.gluu.org/docs/oxdserver/install/)


## Installation
 
### Step 1: Download
[Github source](https://github.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/archive/v2.4.4.zip).

[Link to WordPress marketplace](https://wordpress.org/plugins/openid-connect-sso-by-gluu/)

### Step 2: Upload
Open your WordPress site plugin page, e.g. `https://{site-base-url}/wp-admin/plugin-install.php?tab=upload`, upload the plugin and click on the install now button.

### Step 3: Activate 

Activate the plugin by performing the following steps:
 
1. Go to `https://{site-base-url}/wp-admin/plugins.php`
2. Find OpenID Connect Single Sign On (SSO) Plugin By Gluu and click the activate button.

### Step 4: General
 
In your WP admin menu panel you should now see the OpenID Connect Single Sign On (SSO) Plugin By Gluu menu tab. Click on it.

![General](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/screenshot-1.png) 

1. Membership: must be checked.
2. New User Default Role: please choose user role. 
3. Admin Email: please add your admin email address for registrating the site in the Gluu server.
4. Gluu Server URL: please insert Gluu Server URL.
5. oxd port: choose the port which is using oxd-server (see in `oxd-server/conf/oxd-conf.json` file).
6. Click next to continue.

If you have successfully registered your Gluu Server, you will see bottom page.

![oxd_id](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/screenshot-2.png) 

To make sure everything is configured properly, login to your Gluu Server and navigate to the OpenID Connect > Clients page. Search for your `oxd id`.

### Step 5: OpenID Connect Provider (OP) Configuration

#### Scopes
Scopes are groups of user attributes that are sent from your OP (in this case, the Gluu Server) to the application during login and enrollment. You can view all available scopes in your Gluu Server by navigating to the OpenID Connect > Scopes intefrace. 

In the Plugin interface you can enable, disable and delete scopes. You can also add new scopes. If/when you add new scopes via the plugin, be sure to also add the same scopes in your gluu server. 
![Scopes2](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/screenshot-3.png) 

#### Authentication
To specify the desired authentication mechanism navigate to the Configuration > Manage Custom Scripts menu in your Gluu Server. From there you can enable one of the out-of-the-box authentication mechanisms, such as password, U2F device (like yubikey), or mobile authentication. You can learn more about the Gluu Server authentication capabilities in the [docs](https://gluu.org/docs/multi-factor/intro/).

![Customscripts](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/screenshot-4.png) 

Note:    
- The authentication mechanism specified in your WP plugin page must match the authentication mechanism specified in your Gluu Server.     
- After saving the authentication mechanism in your Gluu Server, it will be displayed in the WP plugin configuration page too.      
- If / when you create a new custom script, both fields are required.       

### Step 6: Wordpress Configuration

#### Current Shortcode
 
You can insert shortcode in the body of the required page/post where you want to display login icons.

Example: ```[gluu_login]```

For Icons you can use request attributes to customize the icons. All attributes are optional.

Example: ```[gluu_login shape="oval" theme="default" space="5" size="40"]```

You can insert shortcode in a PHP file like this:```<?php echo do_shortcode(‘SHORTCODE’) /?>```

Replace the shortcode in the above example code with the required shortcode like ```[gluu_login theme="default"]```, so the final code looks like: 

```
<?php echo do_shortcode('[gluu_login theme="default"]') ?>
```

#### Customize Login Icons
 
If custom scripts are not enabled, nothing will be showed. Customize shape, space between icons and size of the login icons.

#### Display Options
 
1. If you enable the Default Login Form,than login icons will be shown on the WP default login page.
2. If you enable the Default Registration Form, login icons will be shown on the WP default registration page.
3. If you enable the Comment Form, login icons will be shown near the WP Comment Form.
4. If you enable WooCommerce Login Form, login icons will be shown on the WP WooCommerce default login page.

![WordpressConfiguration](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/screenshot-5.png) 

### Step 7: OpenID Connect Single Sign On (SSO) Widget

You can also use this plugin in a WP widget. Navigate to your widget page `https://{site-base-url}/wp-admin/widgets.php` to find and use the OpenID Connect Single Sign On (SSO) Widget.
ht
### Step 8: Show icons in frontend

![frontend](https://raw.githubusercontent.com/GluuFederation/wp_openid_connect_single_sign_on_plugin_by_gluu/master/assets/screenshot-6.png)
