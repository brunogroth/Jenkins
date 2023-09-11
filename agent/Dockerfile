FROM jenkins/jenkins:latest

USER root

RUN apt-get update && apt-get install -y lsb-release

RUN apt-get install python3 pip pipx -y

RUN apt update && apt install python3-pip python3.11-venv -y

RUN apt install python3-fire -y

USER jenkins