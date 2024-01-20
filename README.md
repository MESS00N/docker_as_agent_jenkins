# docker_as_agent_jenkins

**1. Create an EC2 instance**

 * Go to AWS Console
 * Instances(running)
 * Launch instances

   ![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/8d7d21bd-2d85-4fb6-a176-a37283a8124d)



**2. Install Jenkins.**
Pre-Requisites:
Java (JDK)
Run the below commands to install Java and Jenkins
Install Java
```
sudo apt update
sudo apt install openjdk-11-jre
```
Verify Java is Installed
```
java -version
```
Now, you can proceed with installing Jenkins
```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```


![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/c583e345-8b43-463c-92a4-ee54bbf38095)

Jenkins is now running on port 8080

**3. Update Security group of jenkins to 8080**  

![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/536e0a55-dbdd-4087-9255-dcb159c2347c)


Now we should be able to access jenkins


![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/c330136c-6fa4-410b-a01f-3720772ce997)


Need to click on suggested plugins

![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/d867b0e0-e534-449c-b6df-bf5e4fc1d1eb)



![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/9d4d2625-681d-4095-b7ea-e3f4a0a4c943)

![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/12f3f9db-cd79-4a3a-a91c-b64044b2a1a0)



![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/afdfd71e-61aa-4600-9758-60f9ba068d9e)


**4. Install the Docker Pipeline plugin in Jenkins:**

* Log in to Jenkins.
* Go to Manage Jenkins > Manage Plugins.
* In the Available tab, search for "Docker Pipeline".
* Select the plugin and click the Install button.
* Restart Jenkins after the plugin is installed.

![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/8185d871-1b1e-4903-aaa6-b0543fb0489d)

**5.Docker Slave Configuration**

```
sudo apt install docker.io
```
Grant Jenkins user and Ubuntu user permission to docker deamon.

```
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```

The docker agent configuration is now successful.

**6.Creating a new pipeline job**


![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/43e4340b-93eb-4b9c-aec1-40d5f6077276)


**7.Update the jenkins configuration with the git path**

![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/8c29f791-d040-43ef-8ae1-1df97ce84509)



**8. Run the jenkins job**

9. Docker image is created and destroyed

![image](https://github.com/MESS00N/docker_as_agent_jenkins/assets/140514541/5530f16c-47e7-4877-a3aa-223469e7fb30)


10. Console output of the same

'''
Started by user DAA_test
Obtained Jenkinsfile from git https://github.com/MESS00N/docker_as_agent_jenkins.git
[Pipeline] Start of Pipeline
[Pipeline] stage
[Pipeline] { (Back-end)
[Pipeline] node
Running on Jenkins in /var/lib/jenkins/workspace/Docker_as_agent
[Pipeline] {
[Pipeline] checkout
Selected Git installation does not exist. Using Default
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/Docker_as_agent/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/MESS00N/docker_as_agent_jenkins.git # timeout=10
Fetching upstream changes from https://github.com/MESS00N/docker_as_agent_jenkins.git
 > git --version # timeout=10
 > git --version # 'git version 2.34.1'
 > git fetch --tags --force --progress -- https://github.com/MESS00N/docker_as_agent_jenkins.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision ebb008e5c75aac3d68f0b723c914e4de77f21729 (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f ebb008e5c75aac3d68f0b723c914e4de77f21729 # timeout=10
Commit message: "Update Jenkinsfile"
 > git rev-list --no-walk ebb008e5c75aac3d68f0b723c914e4de77f21729 # timeout=10
[Pipeline] withEnv
[Pipeline] {
[Pipeline] isUnix
[Pipeline] withEnv
[Pipeline] {
[Pipeline] sh
+ docker inspect -f . maven:3.8.1-adoptopenjdk-11
.
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] withDockerContainer
Jenkins does not seem to be running inside a container
$ docker run -t -d -u 115:122 -w /var/lib/jenkins/workspace/Docker_as_agent -v /var/lib/jenkins/workspace/Docker_as_agent:/var/lib/jenkins/workspace/Docker_as_agent:rw,z -v /var/lib/jenkins/workspace/Docker_as_agent@tmp:/var/lib/jenkins/workspace/Docker_as_agent@tmp:rw,z -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** maven:3.8.1-adoptopenjdk-11 cat
$ docker top a6b75d6e5974e76428a06df856b68d8507993d275a08feae68fca3253bac989c -eo pid,comm
[Pipeline] {
[Pipeline] sh
+ cd hello-world-app
+ mvn clean package
[INFO] Scanning for projects...
[INFO] 
[INFO] ----------------------< com.mycompany.app:my-app >----------------------
[INFO] Building my-app 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ my-app ---
[INFO] Deleting /var/lib/jenkins/workspace/Docker_as_agent/hello-world-app/target
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ my-app ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /var/lib/jenkins/workspace/Docker_as_agent/hello-world-app/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ my-app ---
[INFO] Changes detected - recompiling the module!
[WARNING] File encoding has not been set, using platform encoding UTF-8, i.e. build is platform dependent!
[INFO] Compiling 1 source file to /var/lib/jenkins/workspace/Docker_as_agent/hello-world-app/target/classes
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ my-app ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /var/lib/jenkins/workspace/Docker_as_agent/hello-world-app/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ my-app ---
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ my-app ---
[INFO] No tests to run.
[INFO] 
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ my-app ---
[INFO] Building jar: /var/lib/jenkins/workspace/Docker_as_agent/hello-world-app/target/my-app-1.0-SNAPSHOT.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  4.425 s
[INFO] Finished at: 2024-01-20T18:29:51Z
[INFO] ------------------------------------------------------------------------
+ mvn test
[INFO] Scanning for projects...
[INFO] 
[INFO] ----------------------< com.mycompany.app:my-app >----------------------
[INFO] Building my-app 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ my-app ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /var/lib/jenkins/workspace/Docker_as_agent/hello-world-app/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ my-app ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ my-app ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /var/lib/jenkins/workspace/Docker_as_agent/hello-world-app/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ my-app ---
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ my-app ---
[INFO] No tests to run.
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  2.002 s
[INFO] Finished at: 2024-01-20T18:29:56Z
[INFO] ------------------------------------------------------------------------
+ java -cp target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.Hello
Hello, World!
[Pipeline] }
$ docker stop --time=1 a6b75d6e5974e76428a06df856b68d8507993d275a08feae68fca3253bac989c
$ docker rm -f --volumes a6b75d6e5974e76428a06df856b68d8507993d275a08feae68fca3253bac989c
[Pipeline] // withDockerContainer
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Front-end)
[Pipeline] node
Running on Jenkins in /var/lib/jenkins/workspace/Docker_as_agent
[Pipeline] {
[Pipeline] checkout
Selected Git installation does not exist. Using Default
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/Docker_as_agent/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/MESS00N/docker_as_agent_jenkins.git # timeout=10
Fetching upstream changes from https://github.com/MESS00N/docker_as_agent_jenkins.git
 > git --version # timeout=10
 > git --version # 'git version 2.34.1'
 > git fetch --tags --force --progress -- https://github.com/MESS00N/docker_as_agent_jenkins.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/main^{commit} # timeout=10
Checking out Revision ebb008e5c75aac3d68f0b723c914e4de77f21729 (refs/remotes/origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f ebb008e5c75aac3d68f0b723c914e4de77f21729 # timeout=10
Commit message: "Update Jenkinsfile"
[Pipeline] withEnv
[Pipeline] {
[Pipeline] isUnix
[Pipeline] withEnv
[Pipeline] {
[Pipeline] sh
+ docker inspect -f . node:16-alpine
.
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] withDockerContainer
Jenkins does not seem to be running inside a container
$ docker run -t -d -u 115:122 -w /var/lib/jenkins/workspace/Docker_as_agent -v /var/lib/jenkins/workspace/Docker_as_agent:/var/lib/jenkins/workspace/Docker_as_agent:rw,z -v /var/lib/jenkins/workspace/Docker_as_agent@tmp:/var/lib/jenkins/workspace/Docker_as_agent@tmp:rw,z -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** node:16-alpine cat
$ docker top 9bfb8b8e648fff29a53307931d2be304ef0030d25303465ba1db7a4c5f373bd9 -eo pid,comm
[Pipeline] {
[Pipeline] sh
+ npm init -y
Wrote to /var/lib/jenkins/workspace/Docker_as_agent/package.json:

{
  "name": "docker_as_agent",
  "version": "1.0.0",
  "description": "**1. Create an EC2 instance**",
  "main": "hello.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/MESS00N/docker_as_agent_jenkins.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/MESS00N/docker_as_agent_jenkins/issues"
  },
  "homepage": "https://github.com/MESS00N/docker_as_agent_jenkins#readme"
}


+ npm install

up to date, audited 1 package in 204ms

found 0 vulnerabilities
+ node hello.js
+ npm start
Hello!  from Node JS
[Pipeline] }
$ docker stop --time=1 9bfb8b8e648fff29a53307931d2be304ef0030d25303465ba1db7a4c5f373bd9
$ docker rm -f --volumes 9bfb8b8e648fff29a53307931d2be304ef0030d25303465ba1db7a4c5f373bd9
[Pipeline] // withDockerContainer
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node
[Pipeline] }
[Pipeline] // stage
[Pipeline] End of Pipeline
Finished: SUCCESS
'''

















  
