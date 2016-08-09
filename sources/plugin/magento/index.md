# Magento GLUU SSO Extension 

![image](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/plugin.png)

MAGENTO-GLUU-SSO extension gives access for login to your Magento site, with the help of GLUU server.

## Install oxD Server
Please use the links below to download the `oxD Server` zip file. For complete installation instructions, please see the [Install Guide](https://oxd.gluu.org/docs/oxdserver/install/)

[oxD Server 2.4.2](https://ox.gluu.org/maven/org/xdi/oxd-server/2.4.2.Final/oxd-server-2.4.2.Final-distribution.zip)

[oxD Server 2.4.3](https://ox.gluu.org/maven/org/xdi/oxd-server/2.4.3.Final/oxd-server-2.4.3.Final-distribution.zip)

[oxD Server 2.4.4](https://ox.gluu.org/maven/org/xdi/oxd-server/2.4.4/oxd-server-2.4.4-distribution.zip)


## Install Magento-gluu-sso Extension
###  Disable cache
 
1. Open menu tab System/Cache Management
![Management](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/mag0.png) 

2. Check select all, set action on disable and click on submit button. 
![submit](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/mag1.png) 

## Install extension

[Magento for Gluu Server 2.4.2](https://github.com/GluuFederation/gluu-magento-sso-login-extension/raw/master/Magento_gluu_SSO_2.4.2.0/Magento_gluu_SSO-2.4.2.0.tgz)

[Magento for Gluu Server 2.4.3](https://github.com/GluuFederation/gluu-magento-sso-login-extension/raw/master/Magento_gluu_SSO_2.4.3.0/Magento_gluu_SSO-2.4.3.0.tgz)

[Magento for Gluu Server 2.4.4](https://github.com/GluuFederation/gluu-magento-sso-login-extension/raw/master/Magento_gluu_SSO_2.4.4/Magento_gluu_SSO-2.4.4.tgz)

1. Open menu tab System/Magento Connect/Magento Connect Manager
![Manager](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/mag2.png) 

2. Choose downloaded file and click on upload button. 
![upload](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/mag3.png) 

3. See Auto-scroll console contents, if extension successfully installed return to admin panel.

3. Open menu tab Gluu SSO/Gluu and Social Login
![GluuSSO](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/mag4.png) 

## Configuration
###  General

![General](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/m1.png)  

1. Admin Email: please add your or admin email address for registrating site in Gluu server.
2. Port number: choose that port which is using oxd-server (see in oxd-server/conf/oxd-conf.json file).
3. Click next to continue.

If You are successfully registered in gluu server, you will see bottom page.

![oxd_id](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/m2.png)

For making sure go to your gluu server / OpenID Connect / Clients and search for your oxD ID

If you want to reset configurations click on Reset configurations button.

### Scopes.
You can look all scopes in your gluu server / OpenID Connect / Scopes and understand the meaning of  every scope.
Scopes are need for getting loged in users information from gluu server.
Pay attention to that, which scopes you are using that are switched on in your gluu server.

In Magento-gluu-sso 2.4.2.0  you can only enable, disable and delete scope.
![Scopes1](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/m3.png) 

In Magento-gluu-sso 2.4.3.0 you can not only enable, disable and delete scope, but also add new scope, but when you add new scope by {any name}, necessary to add that scope in your gluu server too. 
![Scopes2](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/m4.png) 

### Custom scripts.

![Customscripts](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/m5.png)  

You can look all custom scripts in your gluu server / Configuration / Manage Custom Scripts / and enable login type, which type you want.
Custom Script represent itself the type of login, at this moment gluu server supports (U2F, Duo, Google +, Basic) types.

1. Which custom script you enable in your Magento site in order it must be switched on in gluu server too.
2. Which custom script you will be enable in OpenID Connect Configuration page, after saving that will be showed in Magento Configuration page too.
3. When you create new custom script, both fields are required.

## Magento Configuration

### Customize Login Icons
 
Pay attention to that, if custom scripts are not enabled, nothing will be showed.
Customize shape, space between icons and size of the login icons.

![MagentoConfiguration](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/m6.png)  

## Step 10. Show icons in frontend

Go to https://{site-base-url}/index.php/customer/account/login/

![frontend](https://raw.githubusercontent.com/GluuFederation/gluu-magento-sso-login-extension/master/docu/m7.png) 
