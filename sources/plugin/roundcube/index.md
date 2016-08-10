# RoundCube GLUU SSO plugin 
![image](https://raw.githubusercontent.com/GluuFederation/gluu-sso-RoundCube-plugin/master/plugin.jpg)

RoundCube-GLUU-SSO plugin gives access for login to your RoundCube site, with the help of GLUU server.
 
## Requirements
The Opencart module requires Gluu Server and the oxd Server.

* [Gluu Server Installation Guide](https://www.gluu.org/docs/deployment/).

* [oxd Server Installation Guide](https://oxd.gluu.org/docs/oxdserver/install/)

## RoundCube Plugin
Log into the oxd Server and navigate to the `General` tab and fill up the form.

![General](https://raw.githubusercontent.com/GluuFederation/gluu-sso-RoundCube-plugin/master/docu/6.png)  

1. Admin Email: please add your or admin email address for registrating site in Gluu server.
2. Port number: choose that port which is using oxd-server (see in oxd-server/conf/oxd-conf.json file).
3. Click ```Next``` to continue.

If You are successfully registered in gluu server, you will see bottom page.

![oxd_id](https://raw.githubusercontent.com/GluuFederation/gluu-sso-RoundCube-plugin/master/docu/7.png)

For making sure go to your gluu server / OpenID Connect / Clients and search for your oxd ID

If you want to reset configurations click on Reset configurations button.

### OpenID Connect Configuration
### Scopes.
You can look all scopes in your gluu server / OpenID Connect / Scopes and understand the meaning of  every scope.
Scopes are need for getting loged in users information from gluu server.
Pay attention to that, which scopes you are using that are switched on in your gluu server.
[Scopes2](https://raw.githubusercontent.com/GluuFederation/gluu-sso-RoundCube-plugin/master/docu/9.png) 

### Custom scripts.

![Customscripts](https://raw.githubusercontent.com/GluuFederation/gluu-sso-RoundCube-plugin/master/docu/10.png)  

You can look all custom scripts in your gluu server / Configuration / Manage Custom Scripts / and enable login type, which type you want.
Custom Script represent itself the type of login, at this moment gluu server supports (U2F, Duo, Google +, Basic) types.

The custom scripts must be enabled on both the RoundCube site and the Gluu Server for proper functioning.
## RoundCube Configuration
### Customize Login Icons
 
Pay attention to that, if custom scripts are not enabled, nothing will be showed.
Customize shape, space between icons and size of the login icons.

![RoundCubeConfiguration](https://raw.githubusercontent.com/GluuFederation/gluu-sso-RoundCube-plugin/master/docu/11.png)  

## Show icons in frontend

![frontend](https://raw.githubusercontent.com/GluuFederation/gluu-sso-RoundCube-plugin/master/docu/12.png) 
