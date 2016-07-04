[TOC]

# oxD Server Installation/Configuration
This page documents the building, installation of the oxD server.

## Build oxD Server
oxD server can be built using Maven.

oxD code is available in  [Github](https://github.com/GluuFederation/oxd). Maven is used to build the code from github. Download the oxD code from github in any method that is suitable. The code can be downloaded directly from [this link](https://github.com/GluuFederation/oxd/archive/master.zip). The following command can be run inside the oxd folder and it will build oxD Server. Please read the [Maven Guide](http://maven.apache.org/download.cgi) to download and install Maven if necessary.

`# mvn clean package`

## Install oxD Server
### Windows
It is not necessary to install oxD in Windows, it can be downloaded and run. The oxD server is available for download from [maven repository](http://ox.gluu.org/maven/org/xdi/oxd-server).

1. Download oxd Server according to you CE installation (for CE 2.4.3 please download oxd 2.4.3)[oxd-server-2.4.3-Final.zip](http://ox.gluu.org/maven/org/xdi/oxd-server/2.4.3.Final/oxd-server-2.4.3.Final-distribution.zip)
2. Unzip the file in `oxd-server` folder. The folder name is for reference only; any other name will work as well.
3. Run `oxd-server/bin/oxd-start.bat`

### Unix
It is not necessary to install oxD in Unix, it can be downloaded and run. The oxD server is available for download from [maven repository](http://ox.gluu.org/maven/org/xdi/oxd-server/).

1. Download xd Server according to you CE installation (for CE 2.4.3 please download oxd 2.4.3)[oxd-server-2.4.3-Final-distribution.zip](http://ox.gluu.org/maven/org/xdi/oxd-server/2.4.3.Final/oxd-server-2.4.3.Final-distribution.zip)
2. Unzip the file in `oxd-server` folder. The folder name is for reference only; any other name will work as well.
3. Run `oxd-server/bin/oxd-start.sh`

### Linux
The Gluu Repository can be used to install oxD Server. The following headings are followed by installation commands that can be copied and used to isntall oxD Server in the desired OS.

#### CentOS 6
```
wget https://repo.gluu.org/centos/Gluu-centos6.repo -O /etc/yum.repos.d/Gluu.repo
wget https://repo.gluu.org/centos/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU
# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU
# yum clean all
# yum install gluu-oxd-server
# service gluu-oxd-server start
```

#### CentOS 7
```
# wget https://repo.gluu.org/centos/Gluu-centos7.repo -O /etc/yum.repos.d/Gluu.repo
# wget https://repo.gluu.org/centos/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU
# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU
# yum clean all
# yum install gluu-oxd-server
# service gluu-oxd-server start
```

#### RHEL 6
```
# wget https://repo.gluu.org/rhel/Gluu-rhel6.repo -O /etc/yum.repos.d/Gluu.repo
# wget https://repo.gluu.org/rhel/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU
# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU
# yum clean all
# yum install gluu-oxd-server
# service gluu-oxd-server start
```

#### RHEL 7
```
# wget https://repo.gluu.org/rhel/Gluu-rhel7.repo -O /etc/yum.repos.d/Gluu.repo
# wget https://repo.gluu.org/rhel/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU
# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU
# yum clean all
# yum install gluu-oxd-server
# service gluu-oxd-server start
```

#### Ubuntu 14.04(trusty)
```
# echo "deb https://repo.gluu.org/ubuntu/ trusty main" > /etc/apt/sources.list.d/gluu-repo.list
# curl https://repo.gluu.org/ubuntu/gluu-apt.key | apt-key add -
# apt-get update
# apt-get install gluu-oxd-server
# service gluu-oxd-server start
```

#### Ubuntu 16.04(xenial)
```
# echo "deb https://repo.gluu.org/ubuntu/ xenial main" > /etc/apt/sources.list.d/gluu-repo.list
# curl https://repo.gluu.org/ubuntu/gluu-apt.key | apt-key add -
# apt-get update
# apt-get install gluu-oxd-server
# service gluu-oxd-server start
```

#### Debian 8 (Jessie)
```
# echo "deb https://repo.gluu.org/debian/ jessie main" > /etc/apt/sources.list.d/gluu-repo.list
# curl https://repo.gluu.org/debian/gluu-apt.key | apt-key add -
# apt-get update
# apt-get install gluu-oxd-server
# service gluu-oxd-server start
```