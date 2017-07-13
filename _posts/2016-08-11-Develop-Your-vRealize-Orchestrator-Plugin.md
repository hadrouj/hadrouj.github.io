---
published: true
---

This post will help you make your first steps in the desert land of vRO plugin development.

### Prerequisites:
be familiar with vRO basics
Java development basics
maven 3

### Generate a plugin archetype:
access your vRO dev page : https://:8281/vco/develop.jsp
run the maven command to choose interactively an archetype:

    mvn archetype:generate -DarchetypeCatalog=https://<vRO appliance address>:8281/vco-repo/archetype-catalog.xml -DrepoUrl=https://<vRO appliance address>:8281/vco-repo -Dmaven.repo.remote=https://<vRO appliance address>:8281/vco-repo -Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true

before generating the archetype, the previous command will ask for the following parameters :

    type of archetype:

    Choose archetype:
    1: https://<vRO appliance address>:8281/vco-repo/archetype-catalog.xml -> com.vmware.o11n:o11n-archetype-spring (o11nplugin-spring-archetype)
    2: https://<vRO appliance address>:8281/vco-repo/archetype-catalog.xml -> com.vmware.o11n:o11n-plugin-archetype-inventory (o11nplugin-project-archetype)
    3: https://<vRO appliance address>:8281/vco-repo/archetype-catalog.xml -> com.vmware.o11n:o11n-client-archetype-rest (o11nplugin-project-archetype)
    4: https://<vRO appliance address>:8281/vco-repo/archetype-catalog.xml -> com.vmware.o11n:o11n-package-archetype (o11nplugin-project-archetype)
    5: https://<vRO appliance address>:8281/vco-repo/archetype-catalog.xml -> com.vmware.o11n:o11n-plugin-archetype-modeldriven (o11nplugin-project-archetype)
    6: https://<vRO appliance address>:8281/vco-repo/archetype-catalog.xml -> com.vmware.o11n:o11n-archetype-inventory-annotation (o11nplugin-project-archetype)
    7: https://<vRO appliance address>:8281/vco-repo/archetype-catalog.xml -> com.vmware.o11n:o11n-plugin-archetype-simple (o11nplugin-project-archetype)
    Choose a number or apply filter (format: [groupId:]artifactId, case sensitive contains): :

We will choose Number 1 (o11nplugin-spring-archetype)

groupId:

    Define value for property 'groupId': : com.vmware
artifactId:

    Define value for property 'artifactId': : memcached
package:

    Define value for property 'package':  com.vmware: : com.vmware.memcached
pluginAlias:

    Define value for property 'pluginAlias': : Memcached
pluginName:

    Define value for property 'pluginName': : Memcached
confirm the previous info:

    Y: : Y
maven will then build the plugin structure and congratulate you with a:

    [INFO] BUILD SUCCESS
set the package version :

    mvn versions:set -DnewVersion=1.0.1-SNAPSHOT -Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true
change to current directory then build the package :

    mvn clean install -Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true
    the generated plugin can be found in : o11nplugin-memcached/target/o11nplugin-memcached-1.0.0-SNAPSHOT.vmoapp

access the control center -> plugins : https://:8283/vco-controlcenter/#/control-app/plugin-manage

browse to vmoapp location then click install
