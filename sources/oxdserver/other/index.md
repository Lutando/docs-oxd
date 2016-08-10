[TOC]
# Further Reading
# Running oxd Server Manually
These instructions are running the oxd Server manually.

1. Download [oxd distrubution](http://ox.gluu.org/maven/org/xdi/oxd-server/2.4.4-SNAPSHOT/oxd-server-2.4.4-SNAPSHOT-distribution.zip) and **unzip** it.

2. Download the [resteasy jar](http://ox.gluu.org/maven/org/jboss/resteasy/resteasy-jaxrs/2.3.4.Final/resteasy-jaxrs-2.3.4.Final.jar) and [castle jar](http://ox.gluu.org/maven/org/bouncycastle/bcprov-jdk16/1.46/bcprov-jdk16-1.46.jar).

3. Run `java -cp bcprov-jdk16-1.46.jar;resteasy-jaxrs-2.3.4.Final.jar;oxd-server-1.3-SNAPSHOT-jar-with-dependencies.jar org.xdi.oxd.server.ServerLauncher`

The following screen is similar to what you will see if the `oxd Server` start successfully.
![image](http://ox.gluu.org/lib/exe/fetch.php?media=oxd:oxd_started.png)

### Manually with Advanced Configuration
The custom configurations can be loaded using the `oxd.server.config` system property. This property is used to point to the custom configuration `json` file while running the `oxd Server`. The example shoes the location of the custom configurtion to be `C:\tmp\oxd.json`

1. Download [oxd distrubution](http://ox.gluu.org/maven/org/xdi/oxd-server/2.4.4-SNAPSHOT/oxd-server-2.4.4-SNAPSHOT-distribution.zip) and **unzip** it.

2. Download the [resteasy jar](http://ox.gluu.org/maven/org/jboss/resteasy/resteasy-jaxrs/3.0.16.Final/resteasy-jaxrs-3.0.16.Final.jar) and [castle jar](http://ox.gluu.org/maven/org/bouncycastle/bcprov-jdk16/1.46/bcprov-jdk16-1.46.jar).

3. Run `ava -cp resteasy-jaxrs-2.3.4.Final.jar;oxd-server-1.0-SNAPSHOT-jar-with-dependencies.jar org.xdi.oxd.server.ServerLauncher -Doxd.server.config=C:\tmp\oxd.json -Dlog4j.configuration=C:\tmp\test\log4j.xml`

# Troubleshooting
## Windows Java Path Setting

* Java must be in your `PATH` for the `oxd Server` to work. Please check the `java-version` to be sure. The `oxd Server` can be run with the full path to the `java.exe` instead of using `java` in the command.

![image](http://ox.gluu.org/lib/exe/fetch.php?media=oxd:java_installed.png)

* The required JDK version is 1.6 or higher otherwise the following exception might be thrown
```
Exception in thread "main" java.lang.UnsupportedClassVersionError: Bad version number in .class file
        at java.lang.ClassLoader.defineClass1(Native Method)
```
