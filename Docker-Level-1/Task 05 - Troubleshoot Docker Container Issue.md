# Task 5: Troubleshoot Docker Container Issue

## Question

An issue has arisen with a static website running in a container named `nautilus` on `App Server 1`. To resolve the issue, investigate the following details:

**Task:**

1. Check if the container's volume `/usr/local/apache2/htdocs` is correctly mapped with the host's volume `/var/www/html`.

2. Verify that the website is accessible on host port `8080` on `App Server 1`. Confirm that the command `curl http://localhost:8080/` works on `App Server 1`.

---

## Solution

1. **SSH into the server**

```bash
ssh tony@stapp01
# password: Ir0nM@n
```

---

2. **Check running container**

```bash
docker ps
```
Look for the container named `nautilus`.

Check its port mapping and mounted volumes.

---

3. **Inspect container**

Inspect the container:

```bash
docker inspect nautilus
```
Look for:
- **Mounts** → should show something like:

```json
"Mounts": [
  {
    "Type": "bind",
    "Source": "/var/www/html",
    "Destination": "/usr/local/apache2/htdocs"
  }
]
```
- **Ports** → should map host port `8080` to container port `80`:

```json
"HostConfig": {
  "PortBindings": {
    "80/tcp": [
      {
        "HostPort": "8080"
      }
    ]
  }
}
```
If mapping is missing/wrong → that’s the issue.

---

4. **Verify content exists**

Check if website files exist on the **host**:

```bash
ls -l /var/www/html
```
And inside the container:

```bash
docker exec -it nautilus ls -l /usr/local/apache2/htdocs
```
👉 Both should show the same files (since they're volume-mapped).

---

5. **Test website locally**

Run:

```bash
curl http://localhost:8080/
```
Expected: It should return the static page content (like HTML).

If not working:

```bash
docker ps
docker start nautilus
```

---

**✅ Final Check**

```bash
curl http://localhost:8080/
```
Should display the site.