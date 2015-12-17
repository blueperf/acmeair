# WebSphere Liberty Setup Instructions 

If you have not already done so, read through the [instructions for building the codebase](Build_Instructions.md) first. 


## Download the following free for developers or trial versions of WebSphere software

WebSphere Liberty 8.5.5.6
* Download link:  https://developer.ibm.com/wasdev/downloads/liberty-profile-using-non-eclipse-environments
* Click on the "Download Zip" for the "WAS Liberty with Java EE 7 Web Profile" image 
* Review and agree to the license, click the "Accept and download" button and save the resulting "wlp-webProfile7-8.5.5.6.zip" file.


* Install the WebSphere Liberty Profile Developers Runtime file into a directory of your choice
```text
unzip wlp-webProfile7-8.5.5.6.zip
```

* For the rest of these instructions we will assume this to be the WLP_SERVERDIR
Windows:
```text
set WLP_SERVERDIR=C:\work\java\wlp
```
 
Linux:
```text
export WLP_SERVERDIR=~/work/java/wlp
```


## Create the WebSphere Liberty server and then deploy the application(s)
Windows:
```text
cd %WLP_SERVERDIR%
bin\server create acemair
```

Linux:
```text
cd $WLP_SERVERDIR
bin/server create acmeair
```

* Copy the web application you previously built  

Windows:
```text
copy %ACMEAIR_SRCDIR%\acmeair-webapp\build\libs\acmeair-webapp-2.0.0-SNAPSHOT.war %WLP_SERVERDIR%\usr\servers\acmeair\apps\.
```

Linux:
```text
cp $ACMEAIR_SRCDIR/acmeair-webapp/build/libs/acmeair-webapp-2.0.0-SNAPSHOT.war $WLP_SERVERDIR/usr/servers/acmeair/apps/
```

* Change $WLP_SERVERDIR/acmeair/server.xml to:  
```bash
<?xml version="1.0" encoding="UTF-8"?>
<server description="new server">

    <!-- Enable features -->
    <featureManager>
         <feature>jaxrs-2.0</feature>
         <feature>managedBeans-1.0</feature>
         <feature>cdi-1.2</feature>
    </featureManager>

    <!-- To access this server from a remote client add a host attribute to the following element, e.g. host="*" -->
    <httpEndpoint id="defaultHttpEndpoint"
                  host="*"
                  httpPort="9090"
                  httpsPort="9493" />

    <application id="acmeair-webapp" name="acmeair-webapp" type="war" location="acmeair-webapp-2.0.0-SNAPSHOT.war">
      
    </application>

    <jndiEntry jndiName="com/acmeair/repository/type" value="mongo"/>

</server>
```

## MicroService Mode (optional): Create the three additional WebSphere Liberty servers

### Authentication Service

Windows:
```text
cd %WLP_SERVERDIR%
bin\server create acemair-as
```

Linux:
```text
cd $WLP_SERVERDIR
bin/server create acmeair-as
```

* Copy the web application you previously built  

Windows:
```text
copy %ACMEAIR_SRCDIR%\acmeair-as\build\libs\acmeair-as-2.0.0-SNAPSHOT.war %WLP_SERVERDIR%\usr\servers\acmeair-as\apps\.
```

Linux:
```text
cp $ACMEAIR_SRCDIR/acmeair-as/build/libs/acmeair-as-2.0.0-SNAPSHOT.war $WLP_SERVERDIR/usr/servers/acmeair-as/apps/
```

Change $WLP_SERVERDIR/acmeair-as/server.xml to:  
```bash
<?xml version="1.0" encoding="UTF-8"?>
<server description="new server">

    <!-- Enable features -->
    <featureManager>
         <feature>jaxrs-2.0</feature>
         <feature>managedBeans-1.0</feature>
         <feature>cdi-1.2</feature>
    </featureManager>

    <!-- To access this server from a remote client add a host attribute to the following element, e.g. host="*" -->
    <httpEndpoint id="defaultHttpEndpoint"
                  host="*"
                  httpPort="9091"
                  httpsPort="9493" />

    <application id="acmeair-as" name="acmeair-as" type="war" location="acmeair-as-2.0.0-SNAPSHOT.war">
      
    </application>

    <jndiEntry jndiName="com/acmeair/repository/type" value="mongo"/>

</server>
```

### Customer Service

Windows:
```text
cd %WLP_SERVERDIR%
bin\server create acemair-cs
```

Linux:
```text
cd $WLP_SERVERDIR
bin/server create acmeair-cs
```

* Copy the web application you previously built  

Windows:
```text
copy %ACMEAIR_SRCDIR%\acmeair-as\build\libs\acmeair-cs-2.0.0-SNAPSHOT.war %WLP_SERVERDIR%\usr\servers\acmeair-cs\apps\.
```

Linux:
```text
cp $ACMEAIR_SRCDIR/acmeair-as/build/libs/acmeair-cs-2.0.0-SNAPSHOT.war $WLP_SERVERDIR/usr/servers/acmeair-cs/apps/
```

* Change $WLP_SERVERDIR/acmeair-cs/server.xml to:  
```bash
<?xml version="1.0" encoding="UTF-8"?>
<server description="new server">

    <!-- Enable features -->
    <featureManager>
         <feature>jaxrs-2.0</feature>
         <feature>managedBeans-1.0</feature>
         <feature>cdi-1.2</feature>
    </featureManager>

    <!-- To access this server from a remote client add a host attribute to the following element, e.g. host="*" -->
    <httpEndpoint id="defaultHttpEndpoint"
                  host="*"
                  httpPort="9092"
                  httpsPort="9493" />

    <application id="acmeair-cs" name="acmeair-cs" type="war" location="acmeair-cs-2.0.0-SNAPSHOT.war">
      
    </application>

    <jndiEntry jndiName="com/acmeair/repository/type" value="mongo"/>

</server>
```

### Flight Booking Service

Windows:
```text
cd %WLP_SERVERDIR%
bin\server create acemair-fbs
```

Linux:
```text
cd $WLP_SERVERDIR
bin/server create acmeair-fbs
```

* Copy the web application you previously built  

Windows:
```text
copy %ACMEAIR_SRCDIR%\acmeair-fbs\build\libs\acmeair-fbs-2.0.0-SNAPSHOT.war %WLP_SERVERDIR%\usr\servers\acmeair-fbs\apps\.
```

Linux:
```text
cp $ACMEAIR_SRCDIR/acmeair-fbs/build/libs/acmeair-fbs-2.0.0-SNAPSHOT.war $WLP_SERVERDIR/usr/servers/acmeair-fbs/apps/
```

* Change $WLP_SERVERDIR/acmeair-fbs/server.xml to:  
```bash
<?xml version="1.0" encoding="UTF-8"?>
<server description="new server">

    <!-- Enable features -->
    <featureManager>
         <feature>jaxrs-2.0</feature>
         <feature>managedBeans-1.0</feature>
         <feature>cdi-1.2</feature>
    </featureManager>

    <!-- To access this server from a remote client add a host attribute to the following element, e.g. host="*" -->
    <httpEndpoint id="defaultHttpEndpoint"
                  host="*"
                  httpPort="9093"
                  httpsPort="9493" />

    <application id="acmeair-fbs" name="acmeair-fbs" type="war" location="acmeair-fbs-2.0.0-SNAPSHOT.war">
      
    </application>

    <jndiEntry jndiName="com/acmeair/repository/type" value="mongo"/>

</server>
```


## Monolithic Mode - Start the WebSphere Liberty server

* Start the WebSphere Liberty server
Windows:
```text
cd %WLP_SERVERDIR%
bin\server start acmeair
```

Linux:
```text
cd $WLP_SERVERDIR
bin/server start acmeair
```


## MicroService Mode - Start all the WebSphere Liberty servers with env variables

* Start the WebSphere Liberty servers  
Windows:  
```text
cd %WLP_SERVERDIR%
set AUTH_SERVICE=localhost:9091
set CUSTOMER_SERVICE=localhost:9092
set FLIGHTBOOKING_SERVICE=localhost:9093
bin\server.bat start acmeair
bin\server.bat start acmeair-as
bin\server.bat start acmeair-cs
bin\server.bat start acmeair-fbs
```

Linux:
```text
cd $WLP_SERVERDIR
export AUTH_SERVICE=localhost:9091
sexport CUSTOMER_SERVICE=localhost:9092
export FLIGHTBOOKING_SERVICE=localhost:9093
bin/server start acmeair
bin/server start acmeair-as
bin/server start acmeair-cs
bin/server start acmeair-fbs
```

## Look at the application
* Load the following url:
```text
http://localhost:9090/acmeair-webapp
```


## Now we will load sample data using the web loader

* Loader not currently working

