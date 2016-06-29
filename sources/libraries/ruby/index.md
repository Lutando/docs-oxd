#Oxd Ruby
This is the Ruby Client Library for Gluu oxD Server Relaying Party (RP). It is a thin wrapper around the communication protocol of oxD Server which can be used to access the OpenID Connect and UMA Authorization end-points of Gluu Server. his library provides the function calls required by a website to access user information from a OpenID Connect Provider (OP) by using the OxD as the RP.

[Github sources](https://github.com/GluuFederation/oxd-ruby)

[Rubygems](https://rubygems.org/gems/oxd-ruby)

[API Docs](http://www.rubydoc.info/gems/oxd-ruby)

## Installation
### Prerequisite
The Ruby Client library depends on Gluu oxD Server. Please see [this document](https://www.gluu.org/docs-oxd/2.4.4/oxdserver/install/) to install oxD Server.

### Install Instructions
The Ruby Client is installed using RubyGems. Please include following line in the Gemfile of the application using Oxd Ruby Library.

```
gem 'oxd-ruby', '~> 0.1.4'
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
3. config.op_host 
4. config.authorization_redirect_uri

## Using Oxd Ruby
The plugin requires editing the `application_controller.rb` file to include the following snippet.

```
require 'oxd-ruby'

before_filter :set_oxd_commands_instance
protected
    def set_oxd_commands_instance
        @oxd_command = Oxd::ClientOxdCommands.new
        @uma_command = Oxd::UMACommands.new
    end
```

### OP commands sample

```ruby
def register_site		
	if(!@oxd_command.getOxdId.present?)			
		@oxd_command.register_site # Register site and store the returned oxd_id in config
    end
    authorization_url = @oxd_command.get_authorization_url
    redirect_to authorization_url # redirect user to obtained authorization_url to authenticate
end

def login
	if(@oxd_command.getOxdId.present?)
		if (params[:code].present? && params[:state].present?)
			scopes = params[:scope].split("+")
			@access_token = @oxd_command.get_tokens_by_code( params[:code], scopes, params[:state]) 
		end
        session.delete('oxd_access_token') if(session[:oxd_access_token].present?)
    	session[:oxd_access_token] = @access_token
    	session[:state] = params[:state]
    	session[:session_state] = params[:session_state]
		@user = @oxd_command.get_user_info(session[:oxd_access_token]) 			
	end
end

def logout
	if(session[:oxd_access_token])
		@logout_url = @oxd_command.get_logout_uri(session[:oxd_access_token], session[:state], session[:session_state])
		redirect_to @logout_url
	end	    
end
```

### UMA Commands sample

``` ruby
condition1 = {:httpMethods => ["GET"], :scopes => ["http://photoz.example.com/dev/actions/add"]}
condition2 = {:httpMethods => ["GET"], :scopes => ["http://photoz.example.com/dev/actions/view"]}
@uma_command.uma_add_resource("/photo", condition1, condition2)
response = @uma_command.uma_rs_protect # Register above resources with UMA RS
render :template => "uma/index", :locals => { :protect_resources_response => response } 
	
	@uma_command.uma_rp_get_rpt(false) # Get RPT       
response = @uma_command.uma_rs_check_access('/photo', 'GET')        
response = @uma_command.uma_rp_authorize_rpt

scopes = ["http://photoz.example.com/dev/actions/add","http://photoz.example.com/dev/actions/view","http://photoz.example.com/dev/actions/edit"]
gat = @uma_command.uma_rp_get_gat(scopes)
```

## Log Files
The log files for the oxD ruby plugin is stored in the `oxd-ruby.log` file under the `rails_app_root/log` folder. It contains all the logs about oxd-server connections, commands/data sent to server, recieved response and all the errors and exceptions raised.
