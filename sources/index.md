# Welcome to the oxD Documentation

# Introduction

oxd is a mediator: it provides API's that can be called by a web application that are easier
than directly calling the API's of an OpenID Connect provider. oxd is not a proxy--in some 
cases oxd returns URL's for the OP to which the web application must redirect the user. In addition 
to simplying the interface, oxd externalizes the OpenID Connect client code. This may be useful
to some organizations, as it enables update of the OpenID Connect client code, while keeping
the application interface the same.

![image](https://raw.githubusercontent.com/GluuFederation/docs-oxd/master/sources/img/Overview.jpg)

- [oxD Server](./oxdserver/index.md)
- [oxD Libraries] Clients for popular programing languages that call oxd API's and parse the returned JSON.
    - [oxd-java](./plugin/java/index.md) - Java implementation of client
    - [oxd-php](./plugin/php/index.md) - Php implementation of client
    - [oxd-python](./plugin/python/index.md) - Python implementation of client
    - [oxd-node](./plugin/node/index.md) - Node.js implementation of client
    - [oxd-csharp](./plugin/csharp/index.md) - C# implementation of client
- [oxD plugins](./plugin/php/index.md) (more high-level implentation which is based on oxd library.
- [Protocol](./oxdserver/index.md) oxd provides REST API's. If you can't find a client for your language, 
you can write your own by implementing methods for this protocol. 

# Documentation

- [oxD Server](./oxdserver/index.md)
    - [Installation](./oxdserver/install/index.md)
    - [Run](./oxdserver/run/index.md)
    - [Troubleshooting](./oxdserver/troubleshooting/index.md)
- oxD Libraries
    - [Python](./plugin/python/index.md)
    - [PHP](./plugin/php/library/index.md)
    - [Java](./plugin/java/index.md)
    - [Node](./plugin/node/index.md)
    - [Ruby](./plugin/ruby/index.md)
    - [Csharp](./plugin/csharp/index.md)
- [oxD Plugins](./plugin/index.md)
    - [Open Source Plugins](./plugin/php/index.md)
        - [Wordpress plugin](./plugin/php/cms/wordpress/index.md)
        - [Magento extension](./plugin/php/cms/magento/index.md)
        - [Drupal module](./plugin/php/cms/drupal/index.md)
        - [OpenCart module](./plugin/php/cms/opencart/index.md)
        - [SugarCRM module](./plugin/php/crm/sugarcrm/index.md)
        - [SuiteCRM module](./plugin/php/crm/suitecrm/index.md)
        - [RoundCube plugin](./plugin/php/WebMail/roundcube/index.md)
