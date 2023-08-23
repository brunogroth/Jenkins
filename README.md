# Jenkins
Learning Jenkins CI/CD and build, test, and deploy automation.
Those are my personal notes from "Zero to Hero" DevOps Journey's video.

## Functionalities
Jenkins can automate basically any task. 
The web GUI allows to create jobs and customize all functionalities needed, such as source control management, run pre and post build actions as well as build triggers.
You can run tasks on demand when a button is pressed or in a trigger via webhook such as open a bash terminal  and run a Python code.

## Jenkins Infraestructure

### Master Server
- Controls Pipelines
- Schedules Builds

### Agents/Minions
- Run the build (Run linux commands for run & test & distribute the code.

  - **Pernament Agents**: Linux / Windows servers configured to run jenkins jobs (using Java and ssh)
  - **Cloud Agents**: Ephemeral/Dynamic Agents spun up on demand (Docker, Kubernetes, AWS Fleet Manager)

We'll use *Docker* Cloud Agent in here.

### Build Types
  - Freestyle Build: Simplest method (feels like a Shell Script) 
  - Pipelines: uses Groovy Syntax | Use Stages to break down Components of builds (e.g.: stage('Clone') {} stage('Build') {} stage('Test') {} stage('Package') {} stage('Deploy') {}

Sample Build:

![image](https://github.com/brunogroth/Jenkins/assets/96024737/00ab153e-56a9-422f-8550-7074c71d71cd)

# Installation
## Build the Jenkins BlueOcean Docker Image

```
docker build -t myjenkins-blueocean:2.414.1-1 .

```
## Create the network 'jenkins'
```
docker network create jenkins
```

## Run the Image as a Container

```
docker run \
  --name jenkins-blueocean \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.414.1-1
```

Now it's listening on port localhost:8080, you can access it on the browser. To get the password requested on this page, run cat on the docker machine:
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword

## Connect to the Jenkins
```
https://localhost:8080/
```

## Installation Reference:
https://www.jenkins.io/doc/book/installing/docker/

## alpine/socat container to forward traffic from Jenkins to Docker Desktop on Host Machine

https://stackoverflow.com/questions/47709208/how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin
```
docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock
docker inspect <container_id> | grep IPAddress
```
