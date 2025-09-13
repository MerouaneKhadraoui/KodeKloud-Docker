# Task 5: Write a Docker File

## Question

As per recent requirements shared by the Nautilus application development team, they need custom images created for one of their projects. Several of the initial testing requirements are already been shared with DevOps team. Therefore, create a docker file `/opt/docker/Dockerfile` (please keep `D` capital of Dockerfile) on `App server 1` in `Stratos DC` and configure to build an image with the following requirements:

**Task:**

a. Use `ubuntu:24.04` as the base image.

b. Install `apache2` and configure it to work on `3002` port. (do not update any other Apache configuration settings like document root etc).

---

## ✅ Solution Dockerfile

```Dockerfile
# Base image
FROM ubuntu:24.04

# Install Apache2 (non-interactive mode to avoid prompts)
RUN apt-get update && apt-get install -y apache2 

# Change Apache to listen on port 3002
RUN sed -i 's/80/3002/' /etc/apache2/ports.conf && \
    sed -i 's/:80/:3002/' /etc/apache2/sites-available/000-default.conf

# Expose port 3002
EXPOSE 3002

# Run Apache in foreground (so container doesn't exit)
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
```

---

## 🔎 Explanation

1. **Base image** → `ubuntu:24.04`.

2. **Install Apache** → `apt-get update && apt-get install -y apache2`.

3. **Change port** →

    - `ports.conf` (main config) → replace `80` with `3002`.

    - `000-default.conf` (default virtual host) → replace `:80` with `:3002`.

    ⚠️ We **don’t touch document root or other configs**, only the port.

4. **Expose port** → `EXPOSE 3002` tells Docker which port to use.

5. **Foreground run** → `apache2ctl -D FOREGROUND` keeps Apache running in the container.

---

## 🚀 How to test

On `App Server 2`:

```bash
cd /opt/docker
docker build -t custom-apache .

docker images
#custom-apache   latest    8d883127d2b0   12 seconds ago   246MB

docker run -d -p 3002:3002 custom-apache
```

Then run:

```bash
curl http://localhost:3002
```