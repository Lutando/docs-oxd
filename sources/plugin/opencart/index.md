# OPENCART OpenID Connect Single Sign-On (SSO) Extension by Gluu 
## Link to OpenCart marketplace  

[Go to OpenCart marketplace](http://www.opencart.com/index.php?route=extension/extension/info&extension_id=27180&filter_search=Gluu).

OpenID Connect Single Sign-On (SSO) Extension by Gluu gives access for login to your OpenCart site, with the help of GLUU server.
This module will only work on the `https` protocol.

## Requirements
The Opencart module requires Gluu Server and the oxd Server.

* [Gluu Server Installation Guide](https://www.gluu.org/docs/deployment/).

* [oxd Server Installation Guide](https://oxd.gluu.org/docs/oxdserver/install/)

## OPENCART  OpenID Connect Single Sign-On (SSO) Extension by Gluu
 
[Download OpenID Connect Single Sign-On (SSO) Extension by Gluu 2.4.4](https://github.com/GluuFederation/gluu-sso-OpenCart-module/raw/master/Gluu_SSO_2.4.4/Gluu_SSO_2.4.4.zip)

### Install module
 
1. Open menu tab Extensions / Extension Installer and click on ```Upload``` button

2. Choose downloaded module and click on ```Continue``` button. 
![Manager](https://raw.githubusercontent.com/GluuFederation/gluu-sso-OpenCart-module/master/docu/1.png) 

3. Open menu tab Extensions / Modules and find OpenID Connect Single Sign-On (SSO) Extension by Gluu 2.4.v click on ```Install``` button, than click on ```Edit``` button.
![Manager](https://raw.githubusercontent.com/GluuFederation/gluu-sso-OpenCart-module/master/docu/2.png) 

## Configuration
### General

![General](https://raw.githubusercontent.com/GluuFederation/gluu-sso-OpenCart-module/master/docu/6.png)  

In OpenID Connect Single Sign-On (SSO) Extension by Gluu 2.4.4  you need to add Gluu server URL.
![Scopes1](https://raw.githubusercontent.com/GluuFederation/gluu-sso-OpenCart-module/master/docu/15.png) 

1. Admin Email: please add your or admin email address for registrating site in Gluu server.
2. Gluu Server URL: please add your Gluu server URL.
3. Oxd port in your server: choose that port which is using oxd-server (see in oxd-server/conf/oxd-conf.json file).
4. Click next to continue.

If You are successfully registered in gluu server, you will see bottom page.

![oxd_id](https://raw.githubusercontent.com/GluuFederation/gluu-sso-OpenCart-module/master/docu/7.png)

For making sure go to your gluu server / OpenID Connect / Clients and search for your oxd ID

If you want to reset configurations click on Reset configurations button.

### OpenID Connect Configuration

OpenID Connect Configuration page for OpenID Connect Single Sign-On (SSO) Extension by Gluu 2.4.2 and OpenID Connect Single Sign-On (SSO) Extension by Gluu 2.4.3-2.4.4 are different.

#### Scopes.
You can look all scopes in your gluu server / OpenID Connect / Scopes and understand the meaning of  every scope.
Scopes are need for getting loged in users information from gluu server.
Pay attention to that, which scopes you are using that are switched on in your gluu server.

In OpenID Connect Single Sign-On (SSO) Extension by Gluu 2.4.2  you can only enable, disable and delete scope.
![Scopes1](https://raw.githubusercontent.com/GluuFederation/gluu-sso-OpenCart-module/master/docu/8.png) 

In OpenID Connect Single Sign-On (SSO) Extension by Gluu 2.4.3-2.4.4 you can not only enable, disable and delete scope, but also add new scope, but when you add new scope by {any name}, necessary to add that scope in your gluu server too. 
![Scopes2](https://raw.githubusercontent.com/GluuFederation/gluu-sso-OpenCart-module/master/docu/9.png) 

### Custom scripts.

![Customscripts](https://raw.githubusercontent.com/GluuFederation/gluu-sso-OpenCart-module/master/docu/10.png)  

You can look all custom scripts in your gluu server / Configuration / Manage Custom Scripts / and enable login type, which type you want.
Custom Script represent itself the type of login, at this moment gluu server supports (U2F, Duo, Google +, Basic) types.

1. Any custom script enabled in the OpenCart site must be switched on in gluu server.
2. Any custom script enabled in OpenID Connect Configuration page, after saving that will be showed in OpenCart Configuration page.
3. When you create new custom script, both fields are required.

### OpenCart Configuration

#### Customize Login Icons
 
Pay attention to that, if custom scripts are not enabled, nothing will be showed.
Customize shape, space between icons and size of the login icons.

![OpenCartConfiguration](https://raw.githubusercontent.com/GluuFederation/gluu-sso-OpenCart-module/master/docu/11.png)  

### Show icons in frontend

![frontend](https://raw.githubusercontent.com/GluuFederation/gluu-sso-OpenCart-module/master/docu/12.png) 
