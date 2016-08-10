# SugarCRM GLUU SSO module 

![image](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/plugin.jpg)

SugarCRM-GLUU-SSO module gives access for login to your SugarCRM site, with the help of GLUU server.

## Requirements
The Opencart module requires Gluu Server and the oxd Server.

* [Gluu Server Installation Guide](https://www.gluu.org/docs/deployment/).

* [oxd Server Installation Guide](https://oxd.gluu.org/docs/oxdserver/install/)


## SugarCRM-gluu-sso module
Please download the SugarCRM module from the following link:

* [SugarCRM Gluu SSO Module](https://github.com/GluuFederation/gluu-sso-SugarCRM-module/raw/master/SugarCRM_gluu_sso_2.4.4/SugarCRM_gluu_sso_2.4.4.zip)
 
1. Open menu tab Admin and click on ```Module loader``` button
![Manager](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/docu/1.png) 
![Manager](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/docu/2.png) 

2. Choose downloaded module and click on ```Upload``` button. 
![upload](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/docu/d3.png) 

3. Click on ```Install``` button. 
![upload](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/docu/d4.png) 

4. Open menu tab Gluu SSO 2.4.v 
![upload](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/docu/d5.png) 

### General

![General](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/docu/d6.png)  

1. Admin Email: please add your or admin email address for registrating site in Gluu server.
2. Port number: choose that port which is using oxd-server (see in oxd-server/conf/oxd-conf.json file).
3. Click ```Next``` to continue.

If You are successfully registered in gluu server, you will see bottom page.

![oxd_id](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/docu/d7.png)

For making sure go to your gluu server / OpenID Connect / Clients and search for your oxd ID

If you want to reset configurations click on Reset configurations button.

### OpenID Connect Configuration

OpenID Connect Configuration page for SugarCRM-gluu-sso 2.4.2 and SugarCRM-gluu-sso 2.4.3 are different.

#### Scopes.
You can look all scopes in your gluu server / OpenID Connect / Scopes and understand the meaning of  every scope.
Scopes are need for getting loged in users information from gluu server.
Pay attention to that, which scopes you are using that are switched on in your gluu server.
[Scopes2](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/docu/d9.png) 

#### Custom scripts.

![Customscripts](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/docu/d10.png)  

You can look all custom scripts in your gluu server / Configuration / Manage Custom Scripts / and enable login type, which type you want.
Custom Script represent itself the type of login, at this moment gluu server supports (U2F, Duo, Google +, Basic) types.
The custom scripts must be enabled on both the RoundCube site and the Gluu Server for proper functioning.

## Configuration
### Customize Login Icons
 
Pay attention to that, if custom scripts are not enabled, nothing will be showed.
Customize shape, space between icons and size of the login icons.

![SugarCRMConfiguration](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/docu/d11.png)  

### Show icons in frontend

![frontend](https://raw.githubusercontent.com/GluuFederation/gluu-sso-SugarCRM-module/master/docu/d12.png) 
