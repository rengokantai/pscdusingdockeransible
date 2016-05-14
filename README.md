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
copy aws credential and pem file, location:
```
/root/.aws/credentials
/home/ubuntu/.aws/credentials
```
using winscp copy todobackend
```
pip install django
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
using winscp copy todobackend-specs
```
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
npm install
npm install -g mocha
mocha
```
######16
using winscp copy todobackend-client,then
```
cd todobackend-client
npm install
bower install (do not use root user)
```
test
```
http://ip:3000
address=localhost:8000
```
#####4
######23
stage (test)-build-release-deploy
######26
create dockerfile. in entrypoint.sh,
```
exec $@   // get all argument from $1
```
######27(very hard)
```
root@ip-172:/home/ubuntu/todobackend-base# docker build -t rengokantai/todobackend-base .
docker run --rm rengokantai/todobackend-base ps
```
#####31 build dev and release docker image
using winscp copy todobackend,then 
```
cd todobackend
docker build -t todobackend-dev -f docker/dev/Dockerfile .
time docker run --rm todobackend-dev
```

test cache
```
docker run -v /tmp/cache:/cache --entrypoint true --name cache todobackend-dev
```
test time(more efficient)
```
time docker run --rm --volume-from cache todobackend-dev 
```
run in test settings
```
time docker run --rm -e DJANGO_SETTINGS_MODULE=todobackend.settings.test --volume-from cache todobackend-dev 
```
######32 multi container using docker-compose
######33
```
cd docker/dev
docker-compose up test
```
cleanup
```
docker-compose rm -f
```
######34(hard, solve unreliable issue)
using winscp copy  docker-ansible
```
cd docker-ansible
docker build -t rengokantai/ansible .
```
then
```
cd todobackend/docker/dev
docker-compose up agent
docker-compose up test
```
#####5
######40
go to todobackend  
open requirements.txt we can see
```
.
```
because We insall all dependency from install_requires part from setup.py.  
others, see MANIFEST.in, in includes all static files.  
[see here for more](https://docs.python.org/3.5/distutils/sourcedist.html)  
######43
```
cd todobackend/docker/dev
root@ip:/home/ubuntu/todobackend/docker/dev# mv docker-compose.yml docker-compose-v1.yml
root@ip:/home/ubuntu/todobackend/docker/dev# mv docker-compose-v2.yml docker-compose.yml
docker-compose kill
docker-compose rm -f
```
(very important,hard)
```
docker-compose build
docker-compose up agent
docker-compose up test
docker-compose up builder
```
#####6
######47
```
cd todobackend/docker/release
```
######53
```
docker-compose build
docker-comose up agent
docker-compose run --rm app manage.py collectstatic --noinput(squash input)
docker-compose run --rm app manage.py migrate --noinput
```
#####7
######61
make basics
```
make test
make build
```
....
using tab for identation
```
.PHONY: test build release

test:
  echo ""
build:
release:
```
