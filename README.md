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
pip install boto boto3 awscli
```

#####3
######17
```
pip install dangorestframework django-core-headers(tested not working) use:
git clone https://github.com/ottoyiu/django-cors-headers.git
cd django-cors-headers
python setup.py install
```
######18
```
apt-get install mysql-server
mysql -u root -p
create database todobackend;
grant all privileges on *.* to 'todo'@'localhost' identified by 'password';
```
install mysql-python(obsolete,doesnot support python3, using pymysql)
```
apt-get install libmysqlclient-dev python-dev
pip install mysql-python
```
then
```
pip install django-nose
pip install pinocchio
pip install coverage
```
run test
```
python manage.py test --settings=todobackend.settings.test
```
before running mocha test:
```
python manage.py migrate --settings=todobackend.settings.test
python manage.py runserver --settings=todobackend.settings.test
```
go to todobackend-specs
```
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
npm install
npm install -g mocha
mocha
```
