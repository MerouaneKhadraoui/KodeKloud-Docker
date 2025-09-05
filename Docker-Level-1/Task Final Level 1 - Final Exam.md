# Final Exam - Docker Level 1

## Question 1 (Weight: 10)

The Nautilus DevOps team is testing some applications deployment on some of the application servers. They need to deploy a nginx container on `Application Server 3`. Please complete the task as per details given below:

On `Application Server 3` create a container named `nginx_3` using image `nginx` with `alpine` tag and make sure container is in `running` state.

---

## Question 2 (Weight: 10)

The Nautilus team wants to create a debug container on `Application Server 3`. However, they had some specific requirements related to the CMD. Please complete the task as per details given below:

a. On `Application Server 3` create a container named `debug_3` using image `ubuntu/apache2:latest`.

b. Overwrite the default CMD with command `sleep 1000`.

c. Make sure the container is in `running` state.

---

## Question 3 (Weight: 10)

The Nautilus DevOps team has some confidential data present on `App Server 3` in `Stratos Datacenter`. There is a container `ubuntu_latest` running on the same server. We received a request to copy some of the data from the docker host to the container. Below are more details about the task:

On `App Server 3` in `Stratos Datacenter` copy an encrypted file `/tmp/nautilus.txt.gpg` from docker host to `ubuntu_latest` container (running on same server) in `/usr/src/` location (create this location if doesn't exit). Please do not try to modify this file in any way.

## Question 4 (Weight: 12)

We received a request to copy some of the data from one of the docker containers to the docker host. The container is running on `App Server 3` in `Stratos Datacenter`. Below are more details about the task:

On `App Server 3` in `Stratos Datacenter` copy an encrypted file `/tmp/test.txt.gpg` from `development_3` docker container to the docker host in `/tmp` location. Please do not try to modify this file in any way.

---

## Question 5 (Weight: 20)

The Nautilus DevOps team wanted to transfer some docker images from one server to another server so they wanted to save some docker images as tar archives on the docker host itself. Find below the exact requirements:

There is a docker image named `nginx:mainline-alpine-slim` on `App Server 3` in `Stratos Datacenter`, save this image as `nginx.tar` archive under `/home` directory on the same server.

---

## Question 6 (Weight: 10)

There is a docker image on `Application Server 3` in `Stratos DC`. This image needs to be retagged as per details given below:

Re-tag the `nginx:mainline-alpine3.18-slim` image as `nginx:nautilus`

---

## Question 7 (Weight: 10)

The Nautilus DevOps team is planning to setup/create some docker containers on `App Server 3` in `Stratos Datacenter`, some prerequisites are needs to be done on this server. Find below more details:

Create a new network named `mysql-network` using the `bridge` driver. Allocate subnet `182.18.0.0/24`, configure Gateway `182.18.0.1`.

---

## Question 8 (Weight: 10)

The Nautilus DevOps team is planning to do some cleanup on `App Server 3` in `Stratos Datacenter`, some old and unused docker networks need to be deleted. Find below more details:

Delete a docker network named `php-network` from `App Server 3` in `Stratos Datacenter`.

---

## Question 9 (Weight: 10)

There is a static website running within a container named `nautilus`, this container is running on `App Server 3`. Suddenly, we started facing some issues with the static website on `App Server 3`. Look into the issue to fix the same, you can find more details below:

a. Container's volume `/usr/local/apache2/htdocs` is mapped with the host volume `/var/www/html`.

b. The website should run on host port `8080` on `App Server 3` i.e command `curl http://localhost:8080/` should work on `App Server 3`.

---