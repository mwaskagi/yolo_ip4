## Deploy App to Google Kubernetes Engine

#### Base Images
- Used `node:16-alpine` as the base image bacause of its lightweight.
- Used `mongo` image for the database and it size is smaller compared to the `:latest` tag 


#### Dockerfile
- Separate ```Dockerfile``` for each container because each has different package requirements and ports.

#### K8s Objects
- `Backend Deployment YAML`
  - Deployment yaml file for backend application defining its external service of type `LoadBalancer`
  - The backend service accepts requests on port 5000 which forwards to the backend container also running on port 5000
  - I used `ConfigMap` to access `MONGODB_URL` variable which is defined in the mongo-config.yml file.
- `Client Deployment YAML`
  - I created a deployment yaml file for frontend application defining its external service of type `LoadBalancer`
  - The frontend service accepts requests on port 3000 which forwards to the frontend container also running on port 3000
- `Database StatefulSet YAML`
  - I created a statefulset yaml file for mongo db defining its service of type `ClusterIP`
  - The mongo db service will utilize its connectivity with other pods within the cluster network to process and manage application data. Mongo db service is accessible via port 27017
- `Persistent Volume Claim`
  - I created a deployment yaml file for database data persistence.I mapped this on mongo db deployment and a volume.
- I setup [GCLI(Google Cloud CLI)](https://cloud.google.com/sdk/docs/install-sdk)
- Enable APis 
   ```
   gcloud services enable containerregistry.googleapis.com container.googleapis.com

   ```
-  Areate a kubernetes cluster on GKE
    ```
    gcloud container clusters create yolo-app --num-nodes=3 --zone us-central1-a
    ```
- I applied the deployment files using kubectl.
    ```
    kubectl apply -f manifests
    ```
- I used `kubectl cli` to deploy the application to kubernetes. First on minikube and then on Google GKE.