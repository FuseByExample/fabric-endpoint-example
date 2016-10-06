#Fabric Endpoint Example

This project presenta a sample app for the usage of fabric endpoints. It presents a simple client which sends messages 
to the consumer and logs the conversation. The consumer module simply responds to the message of the client. The Client 
adresses the service of the consumer by using a fabric endpoint.

##Project layout

The Maven projects contained within are as follows:

* `client` - The client used to connect to the service
* `consumer` - The module that provides the service trough it's fabric endpoint
* `features` - Contains an XML features file used to simplify the installation of the bundles.

## Requirements:

* JBoss Fuse 6.3.0 (http://www.jboss.org/jbossfuse)
* Maven 3.2.3 or newer (http://maven.apache.org/)
* Java SE 7

## Building the example

Build this project so bundles are deployed into your local maven repo

    <project home> $ mvn clean install

## Prepare Fabric

Start JBoss Fuse and create a fabric

    <JBoss Fuse home>  $ bin/fuse
    JBossFuse:karaf@root> fabric:create --wait-for-provisioning 
    

## Create a profile containing the client and consumer

    JBossFuse:karaf@root> fabric:profile-create --parent feature-camel --parent karaf endpoint-profile
    JBossFuse:karaf@root> fabric:profile-edit --repository mvn:com.fusesource.examples/fabric-endpoint-features/1.0-SNAPSHOT/xml/features endpoint-profile 
    JBossFuse:karaf@root> fabric:profile-edit --feature fabric-endpoint-consumer endpoint-profile
    JBossFuse:karaf@root> fabric:profile-edit --feature fabric-endpoint-client endpoint-profile
    
Add the profile to the root container

    JBossFuse:karaf@root> fabric:container-add-profile root endpoint-profile
 
To see what is happening look at the Fuse log file, either from the console

    JBossFuse:karaf@root> log:tail

   or from the command line

    <JBoss Fuse home> $ tail -f data/log/fuse.log
