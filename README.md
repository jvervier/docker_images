# docker_images

This repository is just a way for me to store useful (for me) Dockerfiles

## java-node-gradle
This docker image is an ubuntu based image with openjdk8, nodejs, gradle, npm and ng angular
The image should be run with -u root to be sure every npm install works fine.
For example in a jenkins pipeline :
						docker {
                            ...
                            args '-u root'
                        }