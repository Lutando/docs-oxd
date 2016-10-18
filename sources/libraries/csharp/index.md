# oxd-csharp

oxd-Csharp is a C# .Net library (DLL) to interact with Gluu's OXD Server. For information about oxD, visit [http://oxd.gluu.org](http://oxd.gluu.org)

## Installation

### Prerequisites

* Visual Studio 2015
* Gluu oxD Server - [Installation docs](https://oxd.gluu.org/docs/install/)

### Library

* *Official Gluu's Nuget Package* - Install using the Visual Studio Nuget package manager console from the Gluu's official Nuget Package. Click [here](https://www.nuget.org/packages/Gluu.Oxd.OxdCSharp/) and follow the installation steps.


## Configuration

The minimal configuration required to get oxd-csharp working:

```
[oxd]
host = 127.0.0.1 //IP represents localhost
port = 8099

[client]
authorization_redirect_uri=https://your.site.org/callback
```

All the required and optional configuration items are with application developer. The oxd-csharp library does not have any specific configuration items itself.