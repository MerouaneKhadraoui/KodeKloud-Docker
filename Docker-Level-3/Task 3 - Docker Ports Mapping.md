# Task 3: Docker Ports Mapping

## Question

The Nautilus DevOps team is planning to host an application on a nginx-based container. There are number of tickets already been created for similar tasks. One of the tickets has been assigned to set up a nginx container on `Application Server 1` in `Stratos Datacenter`. Please perform the task as per details mentioned below:

**Task:**

a. Pull `nginx:alpine-perl` docker image on `Application Server 1`.

b. Create a container named `media` using the image you pulled.

c. Map host port `8086` to container port `80`. Please keep the container in running state.

---

## Solution

1. **SSH into App Server 1**

```bash
ssh tony@stapp01
# password: Ir0nM@n
```

---

2. **Pull the image**

```bash
docker pull nginx:alpine-perl
```

---

3. **Run a container with port mapping**

Map host port `8086` → container port `80`:

```bash
docker run -d --name media -p 8086:80 nginx:alpine-perl
```

- `-d` → run in detached (background) mode.
- `--name media` → container name.
- `-p 8086:80` → map host port `8086` to container port `80`.

---

4. **Verify container is running**

Run: 

```bash
docker ps
```
You should see something like:

```nginx
CONTAINER ID   IMAGE          COMMAND                  PORTS                  NAMES
abc12345       nginx:alpine-perl   "nginx -g 'daemon of…"   0.0.0.0:8086->80/tcp   media
```
Make sure:

---

5. **(Optional) Test nginx page**

From Application Server 3:

```bash
curl http://localhost:8086
```
You should get the default nginx welcome page HTML.

---

🔑 Final Command (if you want it in one go):

```bash
docker pull nginx:alpine-perl && docker run -d --name media -p 8086:80 nginx:alpine-perl
```