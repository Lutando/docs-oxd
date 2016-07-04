
oxd-java is oxD Server client implemented in Java language which acts according to [Protocol](../.././oxdserver/index.md).

[Github sources](https://github.com/GluuFederation/oxd-java)

[Tests on github](https://github.com/GluuFederation/oxd-java/blob/master/src/test/java/org/xdi/oxd/client)

[Jenkins builds](https://ox.gluu.org/jenkins/job/oxd-java/)

[API Documentation (Javadocs)](https://oxd.gluu.org/api-docs/oxd-java/2.4.4)

Sample how to use oxd-java.


```java
 CommandClient client = null;
 try {
     client = new CommandClient(host, port);
     final AuthorizationCodeFlowParams commandParams = new AuthorizationCodeFlowParams();
     commandParams.setClientId(clientId);
     commandParams.setClientSecret(clientSecret);
     commandParams.setDiscoveryUrl(discoveryUrl);
     commandParams.setNonce(UUID.randomUUID().toString());
     commandParams.setRedirectUrl(redirectUrl);
     commandParams.setScope("openid");
     commandParams.setUserId(userId);
     commandParams.setUserSecret(userSecret);

     final Command command = new Command(CommandType.AUTHORIZATION_CODE_FLOW);
     command.setParamsObject(commandParams);
     final AuthorizationCodeFlowResponse resp = client.send(command).dataAsResponse(AuthorizationCodeFlowResponse.class);

     assertNotNull(resp);
     notEmpty(resp.getAccessToken());
     notEmpty(resp.getAuthorizationCode());
     notEmpty(resp.getIdToken());
     notEmpty(resp.getRefreshToken());
     notEmpty(resp.getScope());
 } finally {
     CommandClient.closeQuietly(client);
 }
```

