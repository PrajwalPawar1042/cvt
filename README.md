# cvt

1.virtualbox
2.----------->>>>
🐳 1. docker --version
docker --version
Comment:
This checks the version of Docker installed on your system. It’s a quick way to verify that Docker is installed and working.
________________________________________
🐳 2. docker pull ubuntu
docker pull ubuntu
Comment:
This command downloads the latest Ubuntu image from Docker Hub to your local system. Images are like templates used to create containers.
________________________________________
🐳 3. docker run -it ubuntu bash
docker run -it ubuntu bash
Comment:
This runs an Ubuntu container interactively (-it), allowing you to use the Bash shell. It creates and starts a container from the Ubuntu image.
________________________________________
🐳 4. docker ps -a
docker ps -a
Comment:
Lists all containers, including running, stopped, and exited ones. Useful for checking container status and IDs.
________________________________________
🐳 5. docker stop <container_id>
docker stop <container_id>
Comment:
Stops a running container gracefully. Replace <container_id> with the actual ID from docker ps. Handy for shutting down active containers.
________________________________________
🐳 6. docker rm <container_id>
docker rm <container_id>
Comment:
Removes a container from your system. This is useful for cleaning up unused or exited containers.
 

3-------
. Dockerfile, Docker Image, Run Container
Dockerfile:

# Use base image
FROM ubuntu:20.04

# Install dependencies
RUN apt update && apt install -y nginx

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
Commands:

docker build -t my-nginx-image .        # Create docker image
docker run -d --name my-nginx my-nginx-image   # Run container from image

4-------

. Pull Image from Docker Hub & Manage Container
docker pull httpd                    # a) Pull Apache HTTP Server image
docker create --name webserver httpd  # b) Create container
docker start webserver                # Run/start container
docker stop webserver                 # Stop container


5---
First download minikube and then kubectl
Then on cmd  run commands
Minikube start
1. kubectl get nodes
kubectl get nodes
Comment: Lists all nodes in your cluster (master and workers), and shows their status.
2. kubectl get pods --all-namespaces
kubectl get pods --all-namespaces
Comment: Shows all running pods across namespaces — helpful for debugging or monitoring.
3. kubectl create deployment nginx --image=nginx
kubectl create deployment nginx --image=nginx
Comment: Creates a simple NGINX deployment — a great way to start a test workload.
4. kubectl get deployments
kubectl get deployments
Comment: Shows all deployments currently running — includes the one you just created.
5. kubectl expose deployment nginx --port=80 --type=NodePort
kubectl expose deployment nginx --port=80 --type=NodePort
Comment: Exposes your NGINX deployment so it’s accessible from outside the cluster (via a node port).
6. kubectl delete deployment nginx
kubectl delete deployment nginx
Comment: Deletes the NGINX deployment and all its pods — good for cleanup.

6---------
🐳 Step-by-Step: Create a Pod, Get IP, View Logs
✅ Step 1: Create a Pod
Use kubectl run to create a pod running nginx:
kubectl run my-nginx --image=nginx --restart=Never
•	--image=nginx: Pulls the official NGINX image
•	--restart=Never: Makes it a pod, not a deployment
✅ Step 2: Verify the Pod Is Running
kubectl get pods
You’ll see output like:
NAME        READY   STATUS    RESTARTS   AGE
my-nginx    1/1     Running   0          10s
Make sure STATUS is Running.
✅ Step 3: Get Pod IP Address
kubectl get pod my-nginx -o wide
Look for the IP column, e.g.:
NAME        READY   STATUS    IP           NODE       ...
my-nginx    1/1     Running   10.244.0.10  minikube   ...
✅ IP here is the internal cluster IP of the pod.
✅ Step 4: Troubleshoot with Logs
If your pod isn't working, check its logs:
kubectl logs my-nginx
This shows the stdout/stderr output from the pod. NGINX may not output much unless there’s a problem, but it’s crucial for apps that crash or have errors.
________________________________________
✅ Bonus: Exec Into the Pod (Optional)
To manually explore or debug:
kubectl exec -it my-nginx -- /bin/bash


