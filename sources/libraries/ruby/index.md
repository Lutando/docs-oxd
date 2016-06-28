#Oxd Ruby
This is the Ruby Client Library for Gluu oxD Server Relaying Party (RP). It is a thin wrapper around the communication protocol of oxD Server which can be used to access the OpenID Connect and UMA Authorization end-points of Gluu Server. his library provides the function calls required by a website to access user information from a OpenID Connect Provider (OP) by using the OxD as the RP.

## Installation
### Prerequisite
The Ruby Client library depends on Gluu oxD Server. Please see [this document](https://www.gluu.org/docs-oxd/2.4.4/oxdserver/install/) to install oxD Server.

### Install Instructions
The Ruby Client is installed using RubyGems. Please include following line in the Gemfile of the application using Oxd Ruby Library.

```
gem 'oxd-ruby', '~> 0.1.2'
```

Please run the bundle command after to install the `oxd-ruby` plugin.

```
$ bundle install
```

## Configuration
The configurations must be generated first using the following command.

```
$ rails generate oxd:config
```

This command will install the `oxd_config.rb` initializer file in the `config/initializers` directory which contains all the global configuration options for the ruby plugin. The following configurations must be set before the plugin can be used.

1. config.oxd_host_ip
2. config.oxd_host_port
3. config.authorization_redirect_uri

## Using Oxd Ruby
The plugin requires editing the `application_controller.rb` file to include the following snippet.

```
require 'oxd-ruby'

before_filter :set_oxd_commands_instance
protected
    def set_oxd_commands_instance
        @oxd_command = Oxd::ClientOxdCommands.new
    end
```

The `ClientOxdCommands` class of the library provides all the methods required for the website to communicate with the oxD RP through sockets.

### Website Registration
The website can be registered with the OP using the `@oxd_command.register_site` call.

### Authorization URL
An authorizaiton URL is the URL that the user will visit to authorize the application to use the information from the OP such as Gluu Server.

```
authorization_url = @oxd_command.get_authorization_url
```

Using the above url the website can redirect the user for authentication at the OP.

### Access Token
The website needs to parse the information from the callback url and pass it on to get the access token for fetching user information.

```
code = params[:code]
state = params[:state]
scopes = params[:scope].split("+")
access_token = @oxd_command.get_tokens_by_code( code, scopes, state )
```

The values for code, scopes and state are parsed from the callback url query parameters.

#### User Claims
The Claims or user information fields, made availble by the OP can be fetched using the access token obtained above.

```
user = @oxd_command.get_user_info(access_token)
```

Once the user data is obtained, the various claims supported by the OP can be used as required.

```
<% user.each do |field,value| %>
    <%= "#{field} : #{value}" %>
<% end %>
```

The availability of various claims are completely dependent on the OP.

### Logout
Once the required work is done the user can be logged out of the system.

```
logout_uri = @oxd_command.get_logout_uri(access_token, state, session_state)
```

The user is redirected then to the obtained url to perform logout.

## Log Files
The log files for the oxD ruby plugin is stored in the `oxd-ruby.log` file under the `rails_app_root/log` folder. It contains all the logs about oxd-server connections, commands/data sent to server, recieved response and all the errors and exceptions raised.
