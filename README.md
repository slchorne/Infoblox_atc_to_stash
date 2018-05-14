# Infoblox_atc_to_stash
A customized logstash container that pull security domain matches from Infoblox ATC API at a regular interval,then parse and split the events,befor sending them to a syslog server 
## Prerequises
This setup has been tested on Ubuntu 16.04.1 LTS server + docker version 18.03.0-ce

### 1 - install docker,

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt-get update

apt-cache policy docker-ce

sudo apt-get install -y docker-ce

sudo systemctl status docker

sudo docker version

### 2 - pull logstash image
docker pull docker.elastic.co/logstash/logstash:6.2.3

### 2 - pull config files
git clone https://github.com/aca2328/Infoblox_atc_to_stash.git


## How to
From the local repository folder, edit logstash.conf and at line 5, replace 00000000000 with the token value you grab from your UserAccount on csp.infoblox.com
(to get the token, Log in to the Cloud Services Portal, At the upper right-hand corner, click your user name and select User Preferences, On the User Preferences page, click Show under API key)

build the working image with : sudo docker build -f dockerfile_stash -t logstash .

run the container with : sudo docker run --rm -it logstash

if evrything ok you may want to comment stdout directive in logstash.conf and run the image in detach mode (-d)
