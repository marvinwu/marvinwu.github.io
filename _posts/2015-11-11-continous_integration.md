---
layout: post
title: Continous Integration
---


---

#### what is a pull request ?

pull request is a request to repo owner, ask them to pull in our code to theirs

#### what is github flow

the whole setup

https://zapier.com/engineering/continuous-integration-jenkins-docker-github/

how to setup jenkins

note you need to install java first

https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu

how to restart jenkins manually ?

service jenkins restart

how to run jenkins using docker

https://hub.docker.com/_/jenkins/

how to setup jenkins with pull request ?

what to do if compilation of lxml failed because of
src/lxml/lxml.etree.c:8:22: fatal error: pyconfig.h: No such file or directory
     #include "pyconfig.h"

apt-get install libxml2-dev libxslt-dev python-dev lib32z1-dev

how to debug plugins in jenkins ?

go to system log file


why i can run docker as jenkins but got 

/var/run/docker.sock: permission denied.

nano /etc/default/docker, add the following line to it:


#### How do I use jenkins to do auto deploy at staging and one key deploy to production ?

[Build Pipeline Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Build+Pipeline+Plugin)

looks interesting, the explaintion is [here](http://zeroturnaround.com/rebellabs/how-to-use-jenkins-for-job-chaining-and-visualizations/)

[Parameterized Trigger Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Parameterized+Trigger+Plugin)

#### How do I use jenkins to build dockers images ?

Looks like you can split up the whole process into different jobs, each job only does one thign

a good reference [here](http://www.focusedsupport.com/blog/beyond-builds-combining-jenkins-and-docker-for-continuously-running-instances/)

#### How can I check whether a docker image with a name bbu-staging is running or not ?



```
service_port = 9000  
mongo_port = 27017  
rabbit_port = 5672

existing=$(docker ps | grep bbu-staging | grep -o "^[0-9a-z]*")  
if [ ! -z "$existing" ]; then  
  docker stop $existing
fi

docker build -t bbu-staging $WORKSPACE  
docker run -d -p $service_port -p $mongo_port -p $rabbit_port bbu-staging  
```

#### why do I get a mark a build as failure in Jenkins?

add this 

`#!/bin/sh`

By default Jenkins take "/bin/sh -xe" and this means -x will print each and every command.And the other option -e, which causes shell to stop running a script immediately when any command exits with non-zero(when any command fails) exit code.

So by adding the "#!/bin/sh" will allow you to execute with no option.


#### How to backup Jenkins 

Back up and restore
All the settings, build logs, artifact archives are stored under the JENKINS_HOME directory. Simply archive this directory to make a back up. Similarly, restoring the data is just replacing the contents of the JENKINS_HOME directory from a back up.

Back ups can be taken without stopping the server, but when you restore, please do stop the server.

#### How to manage jenkins configuration as code ?

[but this is how I want to introduce The Mother and The Father of all Jenkins plugins - Jenkins Job DSL Plugin](http://mgrebenets.github.io/mobile%20ci/2015/01/29/bamboo-vs-jenkins/)


#### What is agile development ?

increased visiblility


#### How do I use Jira to integrate with continous integration ?



##### How do i trigger jenkins only for specified branch ?

you can set the branch specifiedr as

master
or
develop

but bitbucket trigger will trigger all the jobs !

but polling scm will trigger only the specified branch

use

H/5 * * * *


##### How to backup jenkins ?

[a good reference ](http://www.holisticqa.com/2013/11/backing-up-your-jenkins-configuration/)
```
cd /var/lib
tar czf /root/backup/$(date +%Y%m%d-%H%M%S).tar.gz .

`

##### How to make the jenkins job tile match branch name ?

use branch name setter plugin, 

in build enviroments



##### How to make jenkins job config a flat file and can backup it up ?

use DSL jenkins plugin

and check in the configuration into git

![set up a seed job](https://dl.dropboxusercontent.com/spa/8a95omz6xkznrmw/0_6iw6na.png)

[Jenkins Job DSL plugin](https://github.com/jenkinsci/job-dsl-plugin/wiki/User-Power-Moves)

Sample bitbucket code snippet

```
//
// Jenkins Job DSL example to create build projects for Bitbucket branches
//

// Imports
import java.text.DateFormat
import java.text.SimpleDateFormat
import groovy.time.TimeCategory

// URL components
String baseUrl = "https://bitbucket.org/api"
String version = "1.0"
String organization = "neterial"
String repository = "jenkintest"

// Put it all together
String branchesUrl = [baseUrl, version, "repositories", organization, repository, "branches"].join("/")

Boolean enableAuthentication = true

// Create URL
URL url = branchesUrl.toURL()

// Open connection
URLConnection connection = url.openConnection()

if (enableAuthentication) {
    String username = "test"
    String password = "dontwanttoshow"

    // Create authorization header using Base64 encoding
    String userpass = username + ":" + password;
    String basicAuth = "Basic " + javax.xml.bind.DatatypeConverter.printBase64Binary(userpass.getBytes());

    // Set authorization header
    connection.setRequestProperty ("Authorization", basicAuth)
}

// Open input stream
InputStream inputStream = connection.getInputStream()

// Get JSON output
def branchesJson = new groovy.json.JsonSlurper().parseText(inputStream.text)

// Close the stream
inputStream.close()

// Optional: set system proxy
Boolean setProxy = false
if (setProxy) {
    String host = "myproxyhost.com.au"
    String port = 8080

    System.getProperties().put("proxySet", "true");
    System.getProperties().put("proxyHost", host);
    System.getProperties().put("proxyPort", port);
}


// Iterate through branches JSON
branchesJson.each { branchName, details ->
    DateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss")
    Date lastModified = dateFormat.parse(details["timestamp"])

  
        // Branch is valid, create the job for it
        println "Valid branch: ${branchName}"

        def name=branchName.replaceAll('/','-')
        // Configure the job
        job (name) {
            
            // TODO: the rest of Jenkins job configuration
        }
    
}
```

[good tutorial here](http://codeventor.blogspot.hk/2015/07/jenkins-dsl-scripting-part-3.html)

 [api refernece here](https://jenkinsci.github.io/job-dsl-plugin/#method/javaposse.jobdsl.dsl.helpers.ScmContext.git)


#### how do I configure credentials for bitbucket ?

looks like you dont need it, if you configured ssh login on jenkins user, it is automatically enabled


#### what does jira release do ? and how to better use it ?



#### How do I check what issues goes into a release in jira kanban ?


![click Release](https://dl.dropboxusercontent.com/spa/8a95omz6xkznrmw/c8kxp6fx.png)





, and select the release name, you can see what goes into this release

#### how can i output groovy println statement to jenkins screen output ?

#### why I can't access global enviroment from groovy dsl script ?

it is dsl is note and it is not suppose to acess the [global enviroemtn variable](https://issues.jenkins-ci.org/browse/JENKINS-28921)




