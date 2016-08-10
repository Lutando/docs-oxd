# oxd-spring
This is a sample project that demonstrates how to authenticate using Gluu as an authentication provider in spring project.

## Requirements
The oxd-spring requires the Gluu Server and the oxd Server. Please use the following links to install the required components.

* [oxd Server Installation Guide](https://oxd.gluu.org/docs/oxdserver/install/)

* [Gluu Server Installation Guide](https://www.gluu.org/docs/deployment/)


## Install oxd-spring
Clone the oxd-spring Gtthub repo and run the maven command to install and run oxd-spring
```
git clone https://github.com/GluuFederation/oxd-spring.git
cd oxd-spring 
mvn clean package
```

If dependencies are not installed, you can skip the tests
```
mvn clean package -Dmaven.test.skip=true
java -jar target/oxd-spring-0.0.1-SNAPSHOT.jar
```

Point browser to `https://127.0.0.1:8443/`.

***Note:*** oxd-server must run on *localhost* and be bound to port: *8099*, otherwise you'll need to configure `oxd-spring/src/main/resources/application.properties` file.


