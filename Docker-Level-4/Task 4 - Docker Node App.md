# Task 4: Docker Node App

## Question

There is a requirement to Dockerize a Node app and to deploy the same on `App Server 3`. Under `/node_app` directory on `App Server 3`, we have already placed a `package.json` file that describes the app dependencies and `server.js` file that defines a web app framework.

**Task:**

1. Create a `Dockerfile` (name is case sensitive) under `/node_app` directory:

  - Use any `node` image as the base image.
  - Install the dependencies using `package.json` file.
  - Use `server.js` in the `CMD`.
  - Expose port `3004`.

2. The build image should be named as `nautilus/node-web-app`.

3. Now run a container named nodeapp_nautilus using this image.

  - Map the container port `3004` with the host port `8099`.

- Once deployed, you can test the app using a `curl` command on `App Server 3`:

`curl http://localhost:8099`

---

## Solution

1. **Create the Dockerfile**

Go to the `/node_app` directory:

```bash
cd /node_app
```

Now create a Dockerfile with the following content:

```Dockerfile
# Use Node.js base image
FROM node:lts-alpine

# Set working directory
WORKDIR /usr/src/app

# Copy package.json first (for dependency installation)
COPY package.json .

# Install dependencies
RUN npm install

# Copy the rest of the app files
COPY . .

# Expose port 3004
EXPOSE 3004

# Run server.js when container starts
CMD ["node", "server.js"]
```
---

2. **Build the Docker image**

Run:

```bash
docker build -t nautilus/node-web-app .
```
---

3. **Run the container**

Run:

```bash
docker run -d --name nodeapp_nautilus -p 8099:3004 nautilus/node-web-app
```
---

4. **Test the app**

Check if it’s working:

```bash
curl http://localhost:8099
```
If the app is coded correctly, you should get the expected output from `server.js`.

---

🔥 That completes the task.