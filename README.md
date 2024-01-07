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















  
