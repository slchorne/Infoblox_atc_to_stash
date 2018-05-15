# Infoblox_atc_to_stash
A customized logstash container that pulls security domain matches from Infoblox ATC API at a regular intervals, then parses and splits the events, before sending them to a syslog server

## Prerequises

- An Infoblox ATC account and API key
- A destination syslog server
- Docker
- A Docker host system (see below)

This setup has been tested on Ubuntu 16.04.1 LTS server + docker version 18.03.0-ce

## Quickstart

- start docker
- pull the logstash container image
- pull the config files
- edit the config, add your API key
- build and deploy

## How to

### Start docker,

If you don't have a running instance of docker, you can follow their instructions here https://www.docker.com/community-edition, or you can install an Ubuntu image from scratch following the instructions at the end of this document


### Pull logstash image

`docker pull docker.elastic.co/logstash/logstash:6.2.3`

### Pull config files

`git clone https://github.com/aca2328/Infoblox_atc_to_stash.git`

### Edit the config files

From the local repository folder, edit logstash.conf and at line 5, replace 00000000000 with the token value you grab from your UserAccount on csp.infoblox.com

(to get the token, Log in to the Cloud Services Portal, At the upper right-hand corner, click your user name and select User Preferences, On the User Preferences page, click Show under API key)

## Build and deploy

build the working image

  `sudo docker build -f dockerfile_stash -t logstash`

run the container

`sudo docker run --rm -it logstash`

if everything is ok you may want to comment the stdout directive in logstash.conf and run the image in detach mode (-d)

## Creating a host system for docker

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt-get update

apt-cache policy docker-ce

sudo apt-get install -y docker-ce

sudo systemctl status docker

sudo docker version
