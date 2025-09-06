# Task 2: Docker Update Permissions

## Question

One of the Nautilus project developers need access to run docker commands on `App Server 1`. This user is already created on the server. Accomplish this task as per details given below:

**Task:**

User `mark` is not able to run docker commands on `App Server 1` in `Stratos DC`, make the required changes so that this user can run docker commands without `sudo`.

---

## Solution


## Step 1 - SSH into the server

```bash
ssh tony@stapp01
# password: Ir0nM@n
```
---

## Step 2 - Verify that docker is installed and group exists

```bash
getent group docker
```
---

## Step 3 - Add user `mark` to the `docker` group

```bash
sudo usermod -aG docker mark
```
---

## Step 4 - Apply the group change

```bash
su - mark
```
---

## Step 5 - Verify membership

```bash
id mark
```
You should see `docker` in the list of groups.

---

## Step 6 - Test docker access

```bash
docker ps
```
This should work **without sudo**.

---

✅ That’s it! User `mark` can now run Docker commands without `sudo`.