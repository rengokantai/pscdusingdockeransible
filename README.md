#### pscdusingdockeransible
#####cp2, config
For ansible, install 2.0+ using apt
```
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
```
docker machine and docker-compose
```
pip install docker-compose
curl -L https://github.com/docker/machine/releases/download/v0.6.0/docker-machine-`uname -s`-`uname -m` > /usr/local/bin/docker-machine && \
chmod +x /usr/local/bin/docker-machine
```
other tools
```
pip install boto boto3
```
