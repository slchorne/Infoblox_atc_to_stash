# Infoblox_atc_to_stash
A customized logstash container that pull security domain matches from Infoblox ATC API at a regular interval,then parse and split the events,befor sending them to a syslog server 
# Prerequises
This setup has been tested on Ubuntu 16.04.1 LTS server + docker version 18.03.0
# How to
clone on local machine
sudo docker build -f dockerfile_stash -t logstash .
sudo docker run --rm -it logstash
if evrything ok you may want to comment stdout directive in logstash.conf and run the image in detach mode (-d)
