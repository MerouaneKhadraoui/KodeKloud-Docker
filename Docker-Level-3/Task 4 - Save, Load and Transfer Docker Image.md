# Task 4: Save, Load and Transfer Docker Image

## Question

One of the DevOps team members was working on to create a new custom docker image on `App Server 1` in `Stratos DC`. He is done with his changes and image is saved on same server with name `beta:datacenter`. Recently a requirement has been raised by a team to use that image for testing, but the team wants to test the same on App Server 3. So we need to provide them that image on `App Server 3` in `Stratos DC`.

**Task:**

a. On `App Server 1` save the image `beta:datacenter` in an archive.

b. Transfer the image archive to `App Server 3`.

c. Load that image archive on `App Server 3` with same name and tag which was used on `App Server 1`.


`Note:` Docker is already installed on both servers; however, if its service is down please make sure to start it.

---

## Solution

1. **Save the image on App Server 1**

Login to App Server 1 and save the docker image into a .tar archive:

```bash
# On App Server 1
docker save -o /tmp/beta_datacenter.tar beta:datacenter
```
This creates an archive /tmp/beta_datacenter.tar of the image beta:datacenter.

---

2. **Transfer the archive to App Server 3**

From **App Server 1**, copy the archive to **App Server 3** using `scp`:

```bash
# On App Server 1
scp /tmp/beta_datacenter.tar tony@stapp03:/tmp/
```

---

3. **Load the image on App Server 3**

Login to **App Server 3** and load the image:

```bash
# On App Server 3
docker load -i /tmp/beta_datacenter.tar
```

Check that the image is present:

```bash
docker images | grep beta
```

You should see:

```bash
beta    datacenter   <IMAGE_ID>   <CREATED>   <SIZE>
```
---

✅ That’s it! Now `beta:datacenter` is available on App Server 3 with the same name and tag.