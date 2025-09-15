# Task 2: Docker Volumes Mapping

## Question

The Nautilus DevOps team is testing applications containerization, which is supposed to be migrated on docker container-based environments soon. In today's stand-up meeting one of the team members has been assigned a task to create and test a docker container with certain requirements. Below are more details:

**Task:**

a. On `App Server 1` in `Stratos DC` pull `nginx` image (preferably `latest` tag but others should work too).

b. Create a new container with name `media` from the image you just pulled.

c. Map the host volume `/opt/devops` with container volume `/tmp`. There is an `sample.txt` file present on same server under `/tmp`; copy that file to `/opt/devops`. Also please keep the container in running state.

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
docker pull nginx
```

---

3. **Run a container with volume mapping**

- Map host path `/opt/devops` → container path `/tmp`
- Keep the container running (detach mode)

```bash
docker run -d --name media -v /opt/devops:/tmp nginx
```

---

4. **Copy the file (host) to the container**

```bash
cp /tmp/sample.txt /opt/devops/
```

---

5. **Verify the mapping worked**

- Check inside the container:

```bash
docker exec -it media ls /tmp
```
You should see `sample.txt`.

- Check container status:

```bash
docker ps
```
Container media should be listed and running.

---

## 🔎 Final Checkpoints

- `nginx` image pulled ✅
- Container `media` created & running ✅
- Host directory `/opt/devops` mapped to container `/tmp` ✅
- File `/tmp/sample.txt` copied into `/opt/devops` ✅