# TIM+ Reference Implementation Build
This contains instructions for cloning the TIMPlus RI projects and building all components.

## Tools

The following tools are needed to perform the full build

* jq
* Git
* JDK 8


## Clone repositories
Each module of the RI is contained within its own repository.  You can either manually clone each repository, or you could create an automated script to clone all repositories.  If you have access to a Unix based shell, you can run the following command (assuming you have all the command tools installed) to clone all repositories:

`curl -s https://api.github.com/orgs/DirectStandards/repos?per_page=200 | jq .[].git_url | xargs -n 1 git clone`

If you want to build from the development branch, specify that branch using the following command:

`curl -s https://api.github.com/orgs/DirectStandards/repos?per_page=200 | jq .[].git_url | xargs -n 1 git clone -b develop`

## Build Components
All projects use maven pom.xml files for the build lifecyle.  After cloning all repositories, switch to the `timplus-ri-build` directory and run the following command to build all components.  NOTE: All projects use the maven wrapper removing the need to install a specific version of maven.

Linux:
`./mvnw clean install`

Windows:
`mvnw clean install`

## Run The TIM+ Server

The TIM+ server application in contained in the timplus-server-boot project as is packaged as a Spring Boot jar application.  Once the build is successful, you can run the server copying the direct-im-server-<version>.jar file from the timplus-server-boot/target directory to some other directory and executing a java -jar command from the "other" directory.  For example, if the name of the .jar file is direct-im-server-0.0.1-SNAPSHOT.jar, then run the following command.
  
`java -jar direct-im-server-0.0.1-SNAPSHOT.jar`

The default configuration in the TIM+ server creates a domain name 'domain.com.'  You can access the server's configuration web app from the following location:

`http://localhost:9090`

The default username/password is timplus/timplus.
