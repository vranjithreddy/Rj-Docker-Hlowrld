# docker-helloworld
A simple helloworld app for docker

A simple nginx helloworld application that helps you learn docker image pulls. Runs on port :80

To Build image:
```
docker build -t name .
```
To pull this image:
```
docker pull helloworld:latest
```
To run this image:
```
sudo docker tag helloworld:latest ranjith/helloworld:current

sudo docker container run --detach -p 33:80 --name ranjith helloworld:current
```
