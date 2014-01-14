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

* JBoss Fuse 6.1.0 (http://www.jboss.org/jbossfuse)
* Maven 3.x (http://maven.apache.org/)
* Java SE 6

## Building the example

Build this project so bundles are deployed into your local maven repo

    <project home> $ mvn clean install

## Prepare Fabric

Start JBoss Fuse

    <JBoss Fuse home>  $ bin/fuse

Install the febric web-ui feature

    JBossFuse:karaf@root> features:install fabric-webui


## Create consumer Profile and container

Follow the instructions from the ['Managing a Deployment using Fuse Fabric'-guide]
(https://github.com/FuseByExample/docs/blob/master/deploy-using-fabric/README.md) to configure a profile and container 
for the consumer:

* `profile name`: fabric-endpoint-consumer
* `parent profiles`: camel, karaf
* `features file url`: mvn:com.fusesource.examples/fabric-endpoint-features/1.0-SNAPSHOT/xml/features
* Add the feature `fabric-endpoint-consumer` to the profile

Create a child container named `consumer` and assign the `fabric-endpoint-consumer` profile.

## Install Client feature

Add the example's features to the feature list by adding the features file url:

    JBossFuse:karaf@root> features:addurl mvn:com.fusesource.examples/fabric-endpoint-features/1.0-SNAPSHOT/xml/features

Install the `fabric-endpoint-client` feature:

    JBossFuse:karaf@root> features:install fabric-endpoint-client
 
To see what is happening look at the Fuse log file, either from the console

    JBossFuse:karaf@root> log:display

   or from the command line

    <JBoss Fuse home> $ tail -f data/log/fuse.log
