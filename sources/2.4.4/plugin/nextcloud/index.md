[TOC]

# OpenID Connect Single Sign-On (SSO) NextCloud Plugin By Gluu

Gluu's OpenID Connect Single Sign-On (SSO) NextCloud Plugin will enable you to authenticate users against any standard OpenID Connect Provider (OP). If you don't already have an OP you can use Google or [deploy the free open source Gluu Server](https://gluu.org/docs/deployment).  

## Requirements
1. NextCloud min version 11.0.0
2. In order to use the NextCloud plugin you will need a standard OP (like Google or a Gluu Server) and the oxd server.

* [Gluu Server Installation Guide](https://www.gluu.org/docs/deployment/).

* [oxd Webpage](https://oxd.gluu.org)


## Installation
 
### Download

[Github source](https://github.com/GluuFederation/nextcloud-oxd-plugin/master/gluusso.zip).

[Link to NextCloud marketplace](https://apps.nextcloud.com/apps/openid_connect_sso)

### Unzip 
If you have already downloaded the plugin, unzip it to your NextCloud root/apps folder.

### Activate 

Activate the plugin by performing the following steps:
 
1. Go to `https://{site-base-url}/index.php/settings/apps`
2. Navigate to `Not enabled` and find the OpenID Connect SSO Plugin By Gluu. Click the `Enable` button.
![upload](https://raw.githubusercontent.com/GluuFederation/nextcloud-oxd-plugin/master/docu/1.png) 
 
3. Click the drop down arrow near `Apps` in the top navigation bar and select OpenID Connect SSO.             

![upload](https://raw.githubusercontent.com/GluuFederation/nextcloud-oxd-plugin/master/docu/2.png) 

## Configuration

### General
 
In your NextCloud admin menu panel you should now see the OpenID Connect plugin. Click the link to navigate to the General configuration  page:

![General](https://raw.githubusercontent.com/GluuFederation/nextcloud-oxd-plugin/master/docu/3.png) 

#### Server Settings
Add information for your oxd server in the Server Settings fields. 

1. URI of the OpenID Provider: insert the URI of the OpenID Connect Provider.
2. Custom URI after logout: custom URI after logout (for example "Thank you" page).
3. oxd port: enter the oxd-server port (you can find this in the `oxd-server/conf/oxd-conf.json` file).
4. Click `Register` to continue.

If your OpenID Provider supports dynamic registration (the Gluu Server does), no additional steps are required.

If your OpenID Connect Provider doesn't support dynamic client registration (Google does not), you will need to insert your OpenID Provider `client_id` and `client_secret` on the following page.

![General](https://raw.githubusercontent.com/GluuFederation/nextcloud-oxd-plugin/master/docu/4.png) 

To generate your `client_id` and `client_secret` use the redirect uri: `https://{site-base-url}/index.php?option=oxdOpenId`.

> If you are using a Gluu server as your OpenID Provider, you can make sure everything is configured properly by logging into to your Gluu Server, navigate to the OpenID Connect > Clients page. Search for your `oxd id`.

#### Enrollment
1. Automatically register any user with an account in the OpenID Provider: By setting registration to automatic, any user with an account in the OP will be able to register for an account in your NextCloud site. They will be assigned the new user default role specified below.
2. Only register and allow ongoing access to users with one or more of the following roles in the OP: Using this option you can limit registration to users who have a specified role in the OP, for instance `nextcloud`. This is not configurable in all OP's. It is configurable if you are using a Gluu Server. [Follow the instructions below](#role-based-enrollment) to limit access based on an OP role. 
3. Disable Automatic Registration: Choose this option if you do not want to support automatic enrollment. If chosen, the NextCloud admin will need to manually add accounts for users in NextCloud.
4.  New User Default Group: specify which Group to give to new users upon registration.  

##### Enrollment and Access Management
Follow these steps if you are using a Gluu Server as your OP and want to enforce Enrollment and Access Management (i.e. you only want to allow users with a certain role, like `nextcloud`, to register. 

1. Navigate to your Gluu Server admin GUI. 
2. Click the `Users` tab in the left hand navigation menu. 
3. Select `Manage People`. 
4. Find the person(s) who should have access. 
5. Click their user entry. 
6. Add the `User Permission` attribute to the person and specify the same value as in the plugin. For instance, if in the plugin you have limit enrollment to user(s) with role = `nextcloud`, then you should also have `User Permission` = `nextcloud` in the user entry. [See a screenshot example](https://cloud.githubusercontent.com/assets/5271048/19735932/2c3817c4-9b73-11e6-9d59-ace7ecdfed41.png).
7. Update the user record. 
8. Go back to the NextCloud plugin and make sure the `permission` scope is requested (see below). 
9. Now they are ready for enrollment at your NextCloud site. 

### OpenID Connect Configuration

![OpenID Connect Configuration](https://raw.githubusercontent.com/GluuFederation/nextcloud-oxd-plugin/master/docu/5.png)

#### User Scopes

Scopes are groups of user attributes that are sent from the OP to the application during login and enrollment. By default, the requested scopes are `profile`, `email`, and `openid`.  If you are enforcing Enrollment and Access Management, you will also need to request the `User Permission` scope. 

To view your OP's available scopes, open a web browser and navigate to `https://OpenID-Provider/.well-known/openid-configuration`. For example, here are the scopes you can request if you're using [Google as your OP](https://accounts.google.com/.well-known/openid-configuration). 

If you are using a Gluu server as your OpenID Provider, you can view all available scopes by navigating to the OpenID Connect > Scopes interface inside the Gluu Server. 

In the Plugin interface you can enable, disable and delete scopes. 

#### Authentication

Bypass the local NextCloud login page and send users straight to the OP for authentication: Check this box so that when users attempt to login they are sent straight to the OP, bypassing the local NextCloud login screen. When it is not checked, users will see the following screen when trying to login: 

![upload](https://raw.githubusercontent.com/GluuFederation/nextcloud-oxd-plugin/master/docu/6.png) 

Select ACR: To signal which type of authentication should be used, an OpenID Connect client may request a specific authentication context class reference value (a.k.a. "acr"). The authentication options available will depend on which types of mechanisms the OP is configured to support. The Gluu Server supports the following authentication mechanisms out-of-the-box: username/password (basic), Duo Security, Super Gluu, and U2F tokens like Vasco and Yubikey.  

Navigate to your OpenID Provider configuration webpage `https://OpenID-Provider/.well-known/openid-configuration` to see supported `acr_values`. 

In the `Select acr` section of the plugin page, choose the mechanism which you want for authentication. If the `Select acr` value in the plugin is `none`, users will be sent to pass the OP's default authentication mechanism.

