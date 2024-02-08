# TIM+ Reference Implementation Build
This contains instructions for cloning the TIMPlus RI projects and building all components.

## Tools

The following tools are needed to perform the full build

* jq
* Git
* JDK 8


## Clone repositories
Each module of the RI is contained within its own repository.  You can either manually clone each repository, or you could create an automated script to clone all repositories.  If you have access to a Unix based shell, you can run the following command (assuming you have all the command tools installed) to clone all repositories:

`curl -s 'https://api.github.com/orgs/DirectStandards/repos?per_page=200' | jq '.[].clone_url' | grep timplus | xargs -n 1 git clone`

If you want to build from the development branch, specify that branch using the following command:

`curl -s 'https://api.github.com/orgs/DirectStandards/repos?per_page=200' | jq '.[].clone_url' | grep timplus | xargs -n 1 git clone -b develop`

## Build Components
All projects use maven pom.xml files for the build lifecyle.  After cloning all repositories, switch to the `timplus-ri-build` directory and run the following command to build all components.  NOTE: All projects use the maven wrapper removing the need to install a specific version of maven.

Linux:
`./mvnw clean install`

Windows:
`mvnw clean install`

## Run The TIM+ Server

The TIM+ server application in contained in the timplus-server-boot project as is packaged as a Spring Boot jar application.  Once the build is successful, you can run the server by copying the direct-im-server-<version>.jar file from the timplus-server-boot/target directory to some other directory and executing a java -jar command from the "other" directory.  For example, if the name of the .jar file is timplus-server-boot-1.0.0-SNAPSHOT.jar, then run the following command.
  
`java -jar timplus-server-boot-1.0.0-SNAPSHOT.jar`

The default configuration in the TIM+ server creates a domain name 'domain.com.'  You can access the server's configuration web app from the following location:

`http://localhost:9090`

The default username/password is timplus@domain.com/timplus.

For further instructions on deploying and configuring the TIM+ server, refer to the TIM+ server configuration [guide](https://directstandards.github.io/timplus-server-boot/). 

## Run The TIM+ Client
After configuring your TIM+ server with domain, certificates, and users, you can begin connecting to the server with a TIM+ compatible client application.  The TIM+ client is spring boot GUI application that allows you to connect to a server with a configured account and perform many TIM+ actions such as maintaining a contact roster, receiving presence information, sending and receiving TIM+ user to user and group messages, and sending and receiving files.  

Once the build is successful, you can run the client by copying the timplus-client-<version>.jar file from the timplus-client/target directory to some other directory and executing a java -jar command from the "other" directory.  For example, if the name of the .jar file is timplus-client-1.0.0-SNAPSHOT.jar, then run the following command.

`java -jar timplus-client-1.0.0-SNAPSHOT.jar`

The first time you run this application you be prompted for account configuration and login information.  You will most likely want to set the *server* configuration setting to *localhost* to connect to the server running on your local machine.
