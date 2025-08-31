# Task 3: Delete Docker Container

## Question

A container named `kke-container` was created by one of the Nautilus project developers on `App Server 3`. It was solely for testing purposes and now requires deletion. Execute the following task:

**Task:**

Delete the `kke-container` on `App Server 3` in Stratos DC.

---

## Solution

1. **SSH into the server**

```bash
ssh banner@stapp03
# password: BigGr33n
```

---

2. **Verify the container**

Check if the container `kke-container` exists and is running:

```bash
docker ps -a | grep kke-container
```

---

3. **Stop the container (if running)**

If it’s running, stop it first:

```bash
docker stop kke-container
```

---

4. **Delete the container**

Remove it completely:

```bash
docker rm kke-container
```

---

5. **Verify deletion**

Run:

```bash
docker ps -a
```
✅ You should not see `kke-container` anymore.
