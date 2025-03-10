# Dockerizing a Static HTML Page with Nginx

This guide walks you through building, running, and pushing a Docker image that serves a static HTML page using Nginx.

## Prerequisites

- Install [Docker](https://www.docker.com/get-started)
- Create a [Docker Hub](https://hub.docker.com/) account

## Step 1: Create the Required Files

1. **Create an HTML file (`index.html`)** with the following content:

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>Docker Nginx static file</title>
     </head>
     <body>
       <h1>Hello from Nginx inside Docker</h1>
     </body>
   </html>
   ```

2. **Create a Dockerfile (`Dockerfile`)**:

   ```dockerfile
   FROM nginx:alpine
   WORKDIR /usr/share/nginx/html
   COPY . .
   EXPOSE 80
   CMD ["nginx", "-g", "daemon off;"]
   ```

## Step 2: Build the Docker Image

Run the following command to build your Docker image and tag it as `nginx-static:v1`:

```sh
docker build -t nginx-static:v1 .
```

## Step 3: Run a Container from the Image

Run the container and map port 80 of the container to port 8080 on your machine:

```sh
docker run -d -p 8080:80 nginx-static:v1
```

Now, open a browser and visit `http://localhost:8080` to see your static HTML page.

## Step 4: Push the Image to Docker Hub

1. Log in to Docker Hub:

   ```sh
   docker login
   ```

2. Tag the image for Docker Hub (replace `nabaraj123` with your Docker Hub username):

   ```sh
   docker tag nginx-static:v1 nabaraj123/nginx-static:v1
   ```

3. Push the image to Docker Hub:

   ```sh
   docker push nabaraj123/nginx-static:v1
   ```

## Step 5: Enter a Running Container

To explore a running container, use:

```sh
docker exec -it <container_id> sh
```

## Step 6: Manage the Container

1. Run a container in detached mode:

   ```sh
   docker run -d -p 8080:80 nginx-static:v1
   ```

2. Restart the container:

   ```sh
   docker restart <container_id>
   ```

3. Check logs:

   ```sh
   docker logs <container_id>
   ```

## Conclusion

You've successfully built, run, and pushed an Nginx-based static website to Docker Hub! 🚀
