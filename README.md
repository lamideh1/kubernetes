# kubernetes
Comprehensive Documentation: Development of the Basic Frontend Application with Docker and Kubernetes
Project Overview
The goal of this project was to containerize a simple static website (using HTML and CSS) and deploy it on a Kubernetes cluster. The application, which serves as a company's landing page, was containerized using Docker, and then the Docker container was deployed to a Kubernetes cluster for orchestration. The application was accessed through an Nginx server.

1. Initial Setup: Understanding the Requirements
The key objectives of this project were:

Create a simple static website with HTML and CSS.
Dockerize the application to run in a container.
Deploy the Docker container to a Kubernetes cluster for scalability and orchestration.
Use Nginx as the web server to serve the static content.
Access the application via port-forwarding to a local machine.
2. Task Breakdown
Task 1: Set Up Project Directory
The first task involved setting up the basic project structure.

A project directory was created to house all the files and configurations.
Inside this directory, I created two files: index.html and styles.css. These files contained the static content for the landing page, including text, images, and styles.
Rationale: This structure ensured that the content was clearly separated and easily maintainable for the Docker containerization process.

Task 2: Initialize Git
To track changes and ensure version control, I initialized a Git repository in the project directory.

I ran git init to set up the local repository.
This was essential for version control and allowed me to easily manage and track the codebase, especially when pushing to remote repositories later.
Rationale: Using Git ensures traceability and easy collaboration, especially if the project expands or involves multiple developers.

Task 3: Git Commit
After creating the initial HTML and CSS files, I committed the code to Git:

I added all files using git add ..
Then, I committed the changes with a clear message: "Initial commit - HTML and CSS files for the landing page."
Rationale: Committing the code early on ensures that a backup is created and that we have a starting point for version control.

Task 4: Dockerize the Application
This step involved creating a Docker container to encapsulate the static website.

Dockerfile Creation:

I chose to use the official Nginx image as the base for the container since Nginx is a widely used, efficient, and lightweight web server for serving static files.
I copied the index.html and styles.css files into the Nginx HTML directory (/usr/share/nginx/html/), which is where Nginx looks for files to serve.
Building the Docker Image:

Using the docker build command, I created the Docker image from the Dockerfile. This step ensured that the application was correctly containerized and would run consistently in different environments.
Local Testing:

I ran the container using docker run -d -p 8080:80 frontend-app, which made the website available at http://localhost:8080 to verify that the Nginx server was serving the static content correctly.
Rationale: Dockerizing the application ensures that it runs the same way on any machine. It also encapsulates the app with its dependencies, making it easier to deploy on different environments (such as a Kubernetes cluster).

Task 5: Push to Docker Hub
Next, I pushed the Docker image to Docker Hub for remote access and future deployments.

I logged into Docker Hub with docker login.
I tagged the image and pushed it to Docker Hub using the docker push command.
Rationale: Storing the Docker image on Docker Hub allows for easy access and deployment across various platforms, including Kubernetes. It also provides a centralized location for managing images.

Task 6: Set Up a Kind Kubernetes Cluster
To deploy the application in Kubernetes, I set up a local Kubernetes cluster using Kind (Kubernetes in Docker).

First, I installed Kind by downloading and configuring it on my system.
I created a new cluster using the kind create cluster command.
Rationale: Kind allows for setting up a local Kubernetes cluster quickly and efficiently. This provides a development environment for testing Kubernetes deployments before pushing to a cloud-based cluster.

Task 7: Deploy to Kubernetes
After setting up the Kubernetes cluster, I focused on deploying the Dockerized application:

Deployment YAML:

I created a deployment.yaml file that defined the Kubernetes deployment.
This file specified the Docker image, the number of replicas (2 in this case), and the ports to expose for the containers.
I applied the deployment using kubectl apply -f deployment.yaml.

Rationale: The Kubernetes deployment ensures that the application is easily scalable and can be managed as part of a larger, more complex system.

Task 8: Create a Service (ClusterIP)
To expose the application within the cluster, I created a Kubernetes service:

Service YAML:

I defined the service with a ClusterIP type, which is the default and makes the service accessible only inside the cluster.
The service was set up to target port 80 of the deployment.
I applied the service configuration using kubectl apply -f service.yaml.

Rationale: Services in Kubernetes act as a stable endpoint for accessing deployed applications. A ClusterIP service ensures that other Kubernetes resources can communicate with the application.

Task 9: Access the Application
Since the service type was ClusterIP, it wasn’t accessible directly from the local machine. Therefore, I used port-forwarding:

I forwarded the service’s port to my local machine using kubectl port-forward.
I accessed the application by visiting http://localhost:8080.
Rationale: Port-forwarding is a simple way to access a Kubernetes service locally for testing and development. This ensures that everything works as expected before deploying to production.

3. Challenges and Solutions
Challenge 1: Docker Image Configuration:

Ensuring the Docker image had the correct path for the HTML and CSS files was crucial for the container to run correctly. The solution was careful mapping of the paths in the Dockerfile.
Challenge 2: Kubernetes Service Configuration:

Initially, I faced issues with accessing the application because the Kubernetes service was of the wrong type. By using ClusterIP and port-forwarding, I resolved the issue for local testing.
Challenge 3: Docker Push to Docker Hub:

Initially, I struggled with pushing images to Docker Hub due to missing authentication. This was solved by logging into Docker Hub via the CLI using docker login.
4. Benefits of the Approach
Scalability: Kubernetes makes it easy to scale the application by adjusting the replica count in the deployment YAML file.
Portability: Docker ensures that the application runs consistently across different environments, from local development to production.
Modularity: Separating the application into containers and deploying with Kubernetes makes future upgrades or modifications easier.
