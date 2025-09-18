# Task 1: Resolve Dockerfile Issues

## Question

The Nautilus DevOps team is working to create new images per requirements shared by the development team. One of the team members is working to create a `Dockerfile` on `App Server 2` in `Stratos DC`. While working on it she ran into issues in which the docker build is failing and displaying errors. Look into the issue and fix it to build an image as per details mentioned below:

**Task:**

a. The `Dockerfile` is placed on `App Server 2` under `/opt/docker` directory.

b. Fix the issues with this file and make sure it is able to build the image.

c. Do not change base image, any other valid configuration within Dockerfile, or any of the data been used — for example, index.html.


`Note:` Please note that once you click on `FINISH` button all the existing containers will be destroyed and new image will be built from your `Dockerfile`.

```Dockerfile
IMAGE httpd:2.4.43

ADD sed -i "s/Listen 80/Listen 8080/g" /usr/local/apache2/conf/httpd.conf

ADD sed -i '/LoadModule\ ssl_module modules\/mod_ssl.so/s/^#//g' conf/httpd.conf

ADD sed -i '/LoadModule\ socache_shmcb_module modules\/mod_socache_shmcb.so/s/^#//g' conf/httpd.conf

ADD sed -i '/Include\ conf\/extra\/httpd-ssl.conf/s/^#//g' conf/httpd.conf

COPY certs/server.crt /usr/local/apache2/conf/server.crt

COPY certs/server.key /usr/local/apache2/conf/server.key

COPY html/index.html /usr/local/apache2/htdocs/
```

---

## Problems in the given `Dockerfile`

1. `IMAGE` is not a valid Dockerfile instruction → it should be `FROM`.

2. `ADD` cannot be used to run shell commands like `sed`.

- `ADD`/`COPY` are for copying files into the image.
- To run commands inside the container, you must use `RUN`.

3. The path to `httpd.conf` must be absolute (`/usr/local/apache2/conf/httpd.conf`) when running commands.

4. Otherwise, the structure is fine:

- Copying certs
- Copying `index.html` into Apache’s htdocs.

---

## Fixed `Dockerfile`

Here’s the corrected version ✅:

```Dockerfile
FROM httpd:2.4.43

# Change Apache to listen on port 8080
RUN sed -i "s/Listen 80/Listen 8080/g" /usr/local/apache2/conf/httpd.conf

# Enable SSL modules and config
RUN sed -i '/LoadModule ssl_module modules\/mod_ssl.so/s/^#//g' /usr/local/apache2/conf/httpd.conf
RUN sed -i '/LoadModule socache_shmcb_module modules\/mod_socache_shmcb.so/s/^#//g' /usr/local/apache2/conf/httpd.conf
RUN sed -i '/Include conf\/extra\/httpd-ssl.conf/s/^#//g' /usr/local/apache2/conf/httpd.conf

# Copy SSL certificates
COPY certs/server.crt /usr/local/apache2/conf/server.crt
COPY certs/server.key /usr/local/apache2/conf/server.key

# Copy application index.html
COPY html/index.html /usr/local/apache2/htdocs/
```
---

## How to test

On **App Server 2**:

```bash
cd /opt/docker
docker build -t my-httpd .
docker run -d -p 8080:8080 my-httpd
```

Then check:

```bash
curl http://localhost:8080
```
You should see your `index.html`.