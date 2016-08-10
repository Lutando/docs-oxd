# DRUPAL GLUU SSO module 

![image](https://raw.githubusercontent.com/GluuFederation/gluu-sso-drupal-module/master/plugin.jpg)

DRUPAL-GLUU-SSO module gives access for login to your Drupal site, with the help of GLUU server.
The module will not work over `http`, it needs the `https` protocol to function. 

## Install oxd Server
Please use the link below to download the `oxd Server` zip file. For complete installation instructions, please see the [Install Guide](https://oxd.gluu.org/docs/oxdserver/install/)
[oxd Server 2.4.4](https://ox.gluu.org/maven/org/xdi/oxd-server/2.4.4/oxd-server-2.4.4-distribution.zip)

## Install Drupal Module
[Drupal Module 2.4.4](https://github.com/GluuFederation/gluu-sso-drupal-module/raw/master/Drupal_gluu_sso_2.4.4.0/Drupal_gluu_sso_2.4.4.0.tar.gz)

1. Open menu tab Modules and click on `Install new module` button
![Manager](https://raw.githubusercontent.com/GluuFederation/gluu-sso-drupal-module/master/docu/d1.png) 

2. Choose downloaded module and click on `INSTALL` button. 
![upload](https://raw.githubusercontent.com/GluuFederation/gluu-sso-drupal-module/master/docu/d2.png) 

### Activate module
 
1. Go to Modules page
2. Find module Gluu SSO {version}, choose on enabled checkbox and save configuration.
![upload](https://raw.githubusercontent.com/GluuFederation/gluu-sso-drupal-module/master/docu/d3.png) 
3. Go to Configuration page and open module configuration page.
![upload](https://raw.githubusercontent.com/GluuFederation/gluu-sso-drupal-module/master/docu/d4.png) 

## Configuration

![General](https://raw.githubusercontent.com/GluuFederation/gluu-sso-drupal-module/master/docu/d5.png)  

1. Admin Email: please add your or admin email address for registrating site in Gluu server.
2. oxd port in your server: choose that port which is using oxd-server (see in oxd-server/conf/oxd-conf.json file).
3. Click next to continue.

If You are successfully registered in gluu server, you will see bottom page.

![oxd_id](https://raw.githubusercontent.com/GluuFederation/gluu-sso-drupal-module/master/docu/d6.png)

For making sure go to your gluu server / OpenID Connect / Clients and search for your oxd ID

If you want to reset configurations click on Reset configurations button.

### OpenID Connect Configuration
#### Scopes.
You can look all scopes in your gluu server / OpenID Connect / Scopes and understand the meaning of  every scope.
Scopes are need for getting loged in users information from gluu server.
Pay attention to that, which scopes you are using that are switched on in your gluu server.
 
![Scopes2](https://raw.githubusercontent.com/GluuFederation/gluu-sso-drupal-module/master/docu/d8.png) 

#### Custom scripts.

![Customscripts](https://raw.githubusercontent.com/GluuFederation/gluu-sso-drupal-module/master/docu/d9.png)  

You can look all custom scripts in your gluu server / Configuration / Manage Custom Scripts / and enable login type, which type you want.
Custom Script represent itself the type of login, at this moment gluu server supports (U2F, Duo, Google +, Basic) types.

1. Which custom script you enable in your Drupal site in order it must be switched on in gluu server too.
2. Which custom script you will be enable in OpenID Connect Configuration page, after saving that will be showed in Drupal Configuration page too.
3. When you create new custom script, both fields are required.

### Drupal Configuration

#### Customize Login Icons
 
Pay attention to that, if custom scripts are not enabled, nothing will be showed.
Customize shape, space between icons and size of the login icons.

![DrupalConfiguration](https://raw.githubusercontent.com/GluuFederation/gluu-sso-drupal-module/master/docu/d10.png)  

#### Frontend Configuration

![frontend](https://raw.githubusercontent.com/GluuFederation/gluu-sso-drupal-module/master/docu/d11.png) 
