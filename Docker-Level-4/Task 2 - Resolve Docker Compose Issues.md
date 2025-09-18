# Task 2: Resolve Docker Compose Issues

## Question

The Nautilus DevOps team is working to deploy one of the applications on `App Server 2` in `Stratos DC`. Due to a misconfiguration in the docker compose file, the deployment is failing. We would like you to take a look into it to identify and fix the issues. More details can be found below:

**Task:**

a. `docker-compose.yml` file is present on `App Server 2` under `/opt/docker` directory.

b. Try to run the same and make sure it works fine.

c. Please do not change the `container names` being used. Also, do not update or alter any other valid config settings in the compose file or any other relevant data that can cause app failure.


`Note:` Please note that once you click on `FINISH` button all existing running/stopped containers will be destroyed, and your compose will be run.

```yaml
name: myapp

services:
    web:
        image: ./app
        container_name: python
        port:
            - "5000:5000"
        volumes:
            - ./app:/code
        depends_on:
            - redis
    redis_app:
        image: redis
        container_name: redis
```

---

## 🔎 Issues in the given file

1. `name:` **is invalid**

In Compose v3+, you can’t use `name:`. Instead, use `services:` directly. If you want to set a project name, you do it with `-p` flag or `project_name` in `compose.override.yml`.
✅ Fix: Remove `name: myapp`.

2. **Image reference is wrong**

```yaml
image: ./app
```
`image:` must be a valid image name, not a local directory. Since the directory `./app` contains the code, you should use `build:` instead.
✅ Fix: Replace `image: ./app` with `build: ./app`.

3. **Typo in `ports`**

```yaml
port:
    - "5000:5000"
```
It should be `ports`, not `port`.
✅ Fix: Change `port:` → `ports:`.

4. **Service naming mismatch**

In `depends_on`, web depends on `redis`, but the service is actually called `redis_app`.
✅ Fix: Either rename service `redis_app` → `redis`, or update `depends_on: - redis_app`.

---

## ✅ Corrected `docker-compose.yml`

Here’s the corrected version ✅:

```yaml
version: "3.8"

services:
  web:
    build: ./app
    container_name: python
    ports:
      - "5000:5000"
    volumes:
      - ./app:/code
    depends_on:
      - redis

  redis:
    image: redis
    container_name: redis
```

---

## 🚀 How to Test

1. Go to the directory:

```bash
cd /opt/docker
```

2. Run the compose:

```bash
docker compose up
```

3. Verify containers:

```bash
docker ps
```
You should see two running containers:

- `python` (the web app)
- `redis` (redis database)