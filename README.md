# Refactor Udagram App into Microservices and Deploy

# Pre Requisites

1. KubeOne
2. Docker
3. Terraform
3. Kubernetes
3. NodeJS v10.X
4. NPM
5. Travis CI account linked to your GitHub repository
6. AWS Account
7. A domain for Route 53 A/B deployment setup

# Application Components

1. Web Frontend - web based application that captures users' posts, logins and sign up
2. Reverse Proxy - NGINX web server that fronts 2 microservices - Feed and User
2. Feed Microservice - A service that handles CRUD operations for user postings
3. User Microservice - A service that handles user CRUD and user authentication operations

# Deployment Setup

1. Each components is repsented by a Service configuration and Deployment configuration files. 
2. The files can be be located under course-03/udacity-c3-deployment/k8s folder.The files are - *-service.yaml and *-deployment.yaml
3. You also need to ensure the configuration for aws-secret, env-configmap and env-secret is also set.


# How to Build and Deploy
1. Build and Deployment is handled by CI / CD pipeline on Travis CI and is triggered by performing Git Push.
2. Before that please ensure that you updated the tag/version number for docker images, service inside docker-compose-build.yaml, *-service.yaml and *-deployment.yaml files.
3. The docker-compose-build.yaml can be found under course-03/udacity-c3-deployment/docker folder.
4. Once the version is set, you may perform Git add, commit and push.
5. The deployment strategy is RollingUpdate. You may view the pods status using command kubectl get pods.

# How to setup A / B Test
1. Configure frontend-service as a LoadBalancer.
2. Do steps under How To Deploy (refer above section)
3. The routing to A or B environment is controlled by AWS Route 53 using 50-50 weightage rule.
4. Ensure that you have setup a domain under Route 53.
5. Create 2 recordsets where each recordset pointing to the frontend LoadBalancer service External-IP. You can get it from kubectl get svc output.
3. Go to http://your-domain:8100
4. Currently both A and B environment is differentiated by their Menu Bar title. For A environment menu title is Menus and B environment menu title is Menu B