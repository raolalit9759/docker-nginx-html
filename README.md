# docker-nginx-html
docker-nginx-html
=======

Dockerized Nginx with a Simple HTML Page
Overview
This project demonstrates how to Dockerize a simple HTML page using Nginx as the web server. The containerization process involves creating an HTML page, configuring Nginx to serve it, building a Docker image, and running a container that serves the page over HTTP.

The objective is to:

Build a Docker image with Nginx serving a static HTML page. Deploy and run the container. Optionally, push the Docker image to Amazon Elastic Container Registry (ECR).

File Descriptions
1. index.html
This is the simple HTML page that will be served by Nginx inside the Docker container. Content example:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello, Docker!</title>
</head>
<body>
    <h1>Hello, Docker!</h1>
</body>
</html>
2. nginx.conf
This is the Nginx configuration file, which tells Nginx how to serve the index.html page. Configuration example:

events { }

http {
    server {
        listen 80;
        location / {
            root /usr/share/nginx/html;
            index index.html;
        }
    }
}
3. Dockerfile
This file defines the instructions to create the Docker image. It uses the official Nginx base image, copies the index.html and nginx.conf files into the correct locations inside the Docker image, and exposes port 80 to the host. Dockerfile example:

# Use the official Nginx image as the base image
FROM nginx:latest

# Copy the custom HTML file into the container's Nginx directory
COPY index.html /usr/share/nginx/html/index.html

# Copy the custom Nginx configuration file into the container
COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80 for the container
EXPOSE 80

# Start Nginx when the container launches
CMD ["nginx", "-g", "daemon off;"]
Steps to Build and Run the Docker Container
1. Build the Docker image:
Run the following command to build the Docker image from the "Dockerfile":

docker build -t my-nginx-image .
This will create a Docker image named "my-nginx-image".

2. Run the Docker Container:
Once the image is built, run the Docker container with the following command:

docker run -d -p 80:80 my-nginx-image
-d: Run the container in detached mode. -p 80:80: Map port 80 of the container to port 80 on the host machine.

3. Access the HTML Page
Open browser and visit http://localhost/ (or the server's IP address if running on a remote server).

Pushing the Image to AWS ECR
To push the image to AWS ECR, follow these steps:

Login to AWS ECR:

aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 975050024946.dkr.ecr.us-west-2.amazonaws.com
Tag the Docker image:

docker tag my-nginx-image:latest 975050024946.dkr.ecr.us-west-2.amazonaws.com/my-nginx-html:latest
Push the image:

docker push 975050024946.dkr.ecr.us-west-2.amazonaws.com/my-nginx-html:latest
Conclusion
This project demonstrates the basics of Dockerizing a static HTML page using Nginx as the web server. By creating a simple HTML page, configuring Nginx, and building a Docker image, you’ve learned how to deploy lightweight web servers in isolated containers. This is an essential skill for building and deploying modern applications in cloud environments, as Docker provides an efficient way to manage application dependencies and streamline deployment processes.

Contact
If you have any questions, suggestions, or feedback, feel free to reach out:

Name: Lalit Kumar Rao

Email: raolalit9759@gmail.com

GitHub: https://github.com/raolalit9759

