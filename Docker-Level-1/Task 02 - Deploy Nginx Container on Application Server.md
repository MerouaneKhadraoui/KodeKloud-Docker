# Task 2: Deploy Nginx Container on Application Server

## Question

The Nautilus DevOps team is conducting application deployment tests on selected application servers. They require a nginx container deployment on `Application Server 2`. Complete the task with the following instructions:

**Task:**

On `Application Server 2` create a container named `nginx_2` using the `nginx` image with the `alpine` tag. Ensure container is in a `running` state.

---

## Solution

1. **SSH into the server**

```bash
ssh steve@stapp02
# password: Am3ric@
```

---

2. **Pull the nginx alpine image (optional, Docker will auto-pull if not found)**

```bash
docker pull nginx:alpine
```

---

3. **Run the container with the required name**

```bash
docker run -d --name nginx_2 nginx:alpine
```
- `-d` → runs container in background (detached mode)
- `--name nginx_2` → names the container
- `nginx:alpine` → uses the nginx image with the `alpine` tag

---

4. **Verify the container is running**

```bash
docker ps | grep nginx_2
```
You should see the container with status `Up`.

---

🔑 **Final Answer**

On Application Server 2, run:

```bash
docker run -d --name nginx_2 nginx:alpine
```