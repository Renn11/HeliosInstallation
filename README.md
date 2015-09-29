#!/bin/bash

#Read the inserted IP and save it in "ip"
read -p "Put in the IP from your Master-Server (e.g :192.131.201.10) " ip

#Update the server
apt-get update

#Install Zookeeper
sudo apt-get install -y zookeeper

#Execute Zookeeper
apt-get install zookeeperd

#Install Docker
curl -sSL https://get.docker.com/ | sh

#Install Helios
curl -sSL https://spotify.github.io/helios-apt/go | sudo sh -

#Install the Master and Agent for Helios
sudo apt-get install -y helios helios-agent helios-master

#Save the connection from the agent and master in .bashrc 
echo "alias helios='helios -z http://$ip:5801'" >> .bashrc

#Delet Code in helios-agent that are in conflict with Zookeeper 
cd /usr/bin
sed -i".bak" '11,16d' helios-agent

#Reboot the system
reboot
