
oxd-java is oxD Server client implemented in Java language which acts according to [Protocol](../.././oxdserver/index.md).

[Github sources](https://github.com/GluuFederation/oxd-java)

[Tests on github](https://github.com/GluuFederation/oxd-java/blob/master/src/test/java/org/xdi/oxd/client)

[Jenkins builds](https://ox.gluu.org/jenkins/job/oxd-java/)

[API Documentation (Javadocs)](https://oxd.gluu.org/api-docs/oxd-java/2.4.4)

## OpenID Connect - Authorization Code Grant overview

```
1. Register site
2. Get authorization URL (which should be used to redirect end-user to Gluu Server for authentication and authorization)
3. Gluu Server redirects back with code
4. Call get_tokens_by_code to obtain Access & ID Tokens
```

### Register site
```java
 CommandClient client = null;
 try {
     client = new CommandClient(host, port);

     final RegisterSiteParams commandParams = new RegisterSiteParams();
     commandParams.setOpHost(opHost);
     commandParams.setAuthorizationRedirectUri(redirectUrl);
     commandParams.setPostLogoutRedirectUri(postLogoutRedirectUrl);
     commandParams.setClientLogoutUri(Lists.newArrayList(logoutUri));
     commandParams.setScope(Lists.newArrayList("openid", "uma_protection", "uma_authorization"));

     final Command command = new Command(CommandType.REGISTER_SITE);
     command.setParamsObject(commandParams);

     final RegisterSiteResponse site = client.send(command).dataAsResponse(RegisterSiteResponse.class);

     // more code here
 } finally {
     CommandClient.closeQuietly(client);
 }
```

### Get authorization URL
```java
final GetAuthorizationUrlParams commandParams = new GetAuthorizationUrlParams();
commandParams.setOxdId(site.getOxdId());

final Command command = new Command(CommandType.GET_AUTHORIZATION_URL);
command.setParamsObject(commandParams);

final GetAuthorizationUrlResponse resp = client.send(command).dataAsResponse(GetAuthorizationUrlResponse.class);
String authorizationUrl = resp.getAuthorizationUrl());
```

### Get token by code
```java

// after login to Authorization Server (authorizationUrl) it redirects back to redirect_uri (registered by register_site command)
// and returns back code. This code must be used to obtain tokens

final GetTokensByCodeParams commandParams = new GetTokensByCodeParams();
commandParams.setOxdId(site.getOxdId());
commandParams.setCode(code);

final Command command = new Command(CommandType.GET_TOKENS_BY_CODE).setParamsObject(commandParams);

final GetTokensByCodeResponse resp = client.send(command).dataAsResponse(GetTokensByCodeResponse.class);
String accessToken = resp.getAccessToken();
String idToken = resp.getIdToken();

```