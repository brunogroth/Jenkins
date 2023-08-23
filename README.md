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
docker build -t myjenkins-blueocean:2.332.3-1 .

```
