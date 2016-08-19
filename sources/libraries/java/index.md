# oxd-Java

oxd-java is a client library for the Gluu oxd server.

## Installation

* [Github sources](https://github.com/GluuFederation/oxd-java)
* Jar files are available on the [Jenkins build server](https://ox.gluu.org/jenkins/job/oxd-java/ws/target/)
* Maven

## Configuration

There are no configuration files for oxd-java. Redirect URI and
other information is set in the code.

## OpenID Connect Usage

* [Tests on github](https://github.com/GluuFederation/oxd-java/blob/master/src/test/java/org/xdi/oxd/client)
* [API Documentation (Javadocs)](https://oxd.gluu.org/api-docs/oxd-java/2.4.4)

### Register 
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

### Get Authorization URL
```java
final GetAuthorizationUrlParams commandParams = new GetAuthorizationUrlParams();
commandParams.setOxdId(site.getOxdId());

final Command command = new Command(CommandType.GET_AUTHORIZATION_URL);
command.setParamsObject(commandParams);

final GetAuthorizationUrlResponse resp = client.send(command).dataAsResponse(GetAuthorizationUrlResponse.class);
String authorizationUrl = resp.getAuthorizationUrl());
```

### Get Tokens 
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

### Get User Info

```java
        CommandClient client = null;
        try {
            client = new CommandClient(host, port);

            final RegisterSiteResponse site = RegisterSiteTest.registerSite(client, opHost, redirectUrl);
            final GetTokensByCodeResponse tokens = requestTokens(client, site, userId, userSecret);

            GetUserInfoParams params = new GetUserInfoParams();
            params.setOxdId(site.getOxdId());
            params.setAccessToken(tokens.getAccessToken());

            final GetUserInfoResponse resp = client.send(new Command(CommandType.GET_USER_INFO).setParamsObject(params)).dataAsResponse(GetUserInfoResponse.class);
            assertNotNull(resp);
            notEmpty(resp.getClaims().get("sub"));
        } finally {
            CommandClient.closeQuietly(client);
        }


```

### Logout

```java
        CommandClient client = null;
        try {
            client = new CommandClient(host, port);

            final RegisterSiteResponse site = RegisterSiteTest.registerSite(client, opHost, redirectUrl, postLogoutRedirectUrl, "");

            final GetLogoutUrlParams commandParams = new GetLogoutUrlParams();
            commandParams.setOxdId(site.getOxdId());
            commandParams.setIdTokenHint("dummy_token");
            commandParams.setPostLogoutRedirectUri(postLogoutRedirectUrl);
            commandParams.setState(UUID.randomUUID().toString());
            commandParams.setSessionState(UUID.randomUUID().toString()); // here must be real session instead of dummy UUID

            final Command command = new Command(CommandType.GET_LOGOUT_URI).setParamsObject(commandParams);

            final LogoutResponse resp = client.send(command).dataAsResponse(LogoutResponse.class);
            assertNotNull(resp);
            assertTrue(resp.getUri().contains(URLEncoder.encode(postLogoutRedirectUrl, "UTF-8")));
        } finally {
            CommandClient.closeQuietly(client);
        }

```


### Update Site

```java
        CommandClient client = null;
        try {
            client = new CommandClient(host, port);

            Calendar calendar = Calendar.getInstance();
            calendar.add(Calendar.DAY_OF_YEAR, 1);

            // more specific site registration
            final UpdateSiteParams commandParams = new UpdateSiteParams();
            commandParams.setOxdId(oxdId);
            commandParams.setClientSecretExpiresAt(calendar.getTime());
            commandParams.setScope(Lists.newArrayList("profile"));

            final Command command = new Command(CommandType.UPDATE_SITE);
            command.setParamsObject(commandParams);

            UpdateSiteResponse resp = client.send(command).dataAsResponse(UpdateSiteResponse.class);
            assertNotNull(resp);
        } finally {
            CommandClient.closeQuietly(client);
        }
    }
```



