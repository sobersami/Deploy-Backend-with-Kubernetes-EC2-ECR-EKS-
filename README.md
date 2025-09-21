##  Overview
In the project, we will deploy an application's backend with Kubernetes. This project will start from scratch (i.e., launching an EC2 instance ) and then have a live backend deployed.


<img width="975" height="557" alt="image" src="https://github.com/user-attachments/assets/dc228fde-a16e-4554-a18a-89e2668d5fbb" />

---
## Steps 
---

## 1. Set up EKS cluster 
•	Lunch and connect to an EC2
•	Set up an eksctl and your instance with AWS credentials 
•	Create an EKS cluster 
<img width="669" height="319" alt="image" src="https://github.com/user-attachments/assets/fd79be22-4674-4ab5-9a0c-e760ac54b0d3" />

- Launch eksctl with the following commands
<img width="975" height="309" alt="image" src="https://github.com/user-attachments/assets/4fca0866-bd69-47c9-ab5e-0d1dec904b77" />

- Set Up an IAM to EC2 
<img width="975" height="423" alt="image" src="https://github.com/user-attachments/assets/f514bc09-222c-4474-9a78-a959372a8010" />
<img width="975" height="385" alt="image" src="https://github.com/user-attachments/assets/93bb8f59-0324-44bf-a6bc-aad14d71a78b" />

- EKS Cluster Commands (Used eksctl to Create the EKS cluster )
<img width="459" height="363" alt="image" src="https://github.com/user-attachments/assets/15f17d09-0240-467b-a19e-3892ec12eecb" />
<img width="975" height="400" alt="image" src="https://github.com/user-attachments/assets/330f0778-ff64-433a-ad7c-0a9fbcfa69f2" />


## 2. Pull the code for your Backend 
- Make a copy of the backend code in GitHub
<img width="446" height="148" alt="image" src="https://github.com/user-attachments/assets/e9c2cf15-2c81-4fda-80ba-70da3e096465" />
<img width="975" height="151" alt="image" src="https://github.com/user-attachments/assets/b5c01063-a500-4f2a-ba13-b59778676def" />

- Configure git
<img width="975" height="236" alt="image" src="https://github.com/user-attachments/assets/9ad26cb7-175b-42f9-8f4b-820068a8d5bc" />
<img width="975" height="153" alt="image" src="https://github.com/user-attachments/assets/f04e07a1-0dcf-4eda-baa9-9cb68b54dbeb" />



- Clone git Repository to EC2
  
   We retrieved the backend code by cloning our team members' repository on GitHub so we can have a local copy of their work. Pulling code is essential to this deployment because we need to access it to build the container image of it so that Kubernetes will deploy



 
## 3. Build a container Image using the backend code 


In this step, we are going to build a container image of the backend code 

<img width="553" height="239" alt="image" src="https://github.com/user-attachments/assets/12f27bd2-ba21-4fce-88a5-e28dea124be6" />

- We need to install and configure Docker

  <img width="409" height="63" alt="image" src="https://github.com/user-attachments/assets/d53bed23-5844-4a22-aa72-4c6a857f4157" />
  <img width="420" height="64" alt="image" src="https://github.com/user-attachments/assets/8687c2f6-feaa-43a5-951f-1b4785712034" />


- Add EC2 user to the Docker group
  <img width="416" height="65" alt="image" src="https://github.com/user-attachments/assets/8ba0d7c3-a7db-4d8a-ba09-e737d62f1f32" />

- Make sure EC2 user has been added to the Docker group
<img width="975" height="212" alt="image" src="https://github.com/user-attachments/assets/ba87dfff-0cdc-4ff3-a71c-4df5bce1c848" />

- We'll jump back into the application
directory. We'll also run the command
again, to list everything inside, so we can
double-check we're at the right place.

- Run the command below to build our Docker image
  
  <img width="975" height="238" alt="image" src="https://github.com/user-attachments/assets/041b1981-a3f6-4f89-8dec-3c6e7acf8388" />

  

  ## 4. Push our container image to Amazon ECR

  In this step, we will push the container image into a repository that we created in Amazon ECR(Elastic Container Registry). This will allow our container image somewhere to live so that Kubernetes can pull it easily for deployment 

  <img width="553" height="289" alt="image" src="https://github.com/user-attachments/assets/09e902e1-31ad-4dbb-88bf-594f401a2138" />

•	Create an Amazon ECR repository using the command below 

<img width="975" height="218" alt="image" src="https://github.com/user-attachments/assets/78d20cfc-3f97-41b5-8c2d-16058eaa5162" />
<img width="975" height="409" alt="image" src="https://github.com/user-attachments/assets/2c6a0f03-0644-48a6-8099-242d49598112" />

 - NOW, push our container Image to ECR
   
<img width="975" height="342" alt="image" src="https://github.com/user-attachments/assets/ed7ac203-5749-40b8-80b5-cfebfa0b953e" />
<img width="975" height="259" alt="image" src="https://github.com/user-attachments/assets/c7ece8c9-0f8c-47e2-921b-b52e829c2166" />
<img width="975" height="270" alt="image" src="https://github.com/user-attachments/assets/2586f8ec-24b9-4b4e-9974-1eeebecd6c1b" />


- We push our container image to ECR because it facilitates scaling for our deployment, because Kubernetes can easily grab whichever image is tagged latest for each container it creates

<img width="975" height="395" alt="image" src="https://github.com/user-attachments/assets/20ceb6f0-68a0-4f20-bcfe-e47fc0578279" />



## 5. Set up our app for deployment 

In this step, you're going to:

 - Create the Deployment manifest, which gives Kubernetes instructions on deploying our containerized backend to our Kubernetes cluster.
 - Create the Service manifest, which tells Kubernetes how to expose our application and route traffic to it.

- Create a directory for Kubernetes manifest 
<img width="381" height="103" alt="image" src="https://github.com/user-attachments/assets/d15fabfe-03e9-4f4f-a188-31273f6412b0" />
<img width="975" height="127" alt="image" src="https://github.com/user-attachments/assets/1bb1428e-423d-4396-b9af-3883b1a656f7" />

- Create a deployment manifest by running the following command
  It basically tell Kubernetes to how to deploy
  <img width="446" height="625" alt="image" src="https://github.com/user-attachments/assets/0b21c3ad-4131-4209-842b-a3fa2c293040" />
<img width="975" height="284" alt="image" src="https://github.com/user-attachments/assets/275f4652-980b-4b4b-9598-7c7c40aa9db7" />
<img width="975" height="248" alt="image" src="https://github.com/user-attachments/assets/5dc44186-6595-423e-b7bd-0c81c4d434cb" />


- Create a service manifest by running the following command:
  A service manifest exposes deployed application to user/traffic. Our service manifest set up a service resource that exposes our backend application at port 8080 within the EKS cluster

  <img width="359" height="425" alt="image" src="https://github.com/user-attachments/assets/6d0b4560-b5e0-4cbd-a84b-2a18ee9fe5f2" />
<img width="975" height="264" alt="image" src="https://github.com/user-attachments/assets/36431d99-22fd-4981-8fd4-b5a97178c235" />


## 6. Deploying our backend application

In this step, we will deploy the application using kubectl, a command-line tool for creating and managing Kubernetes resources.

<img width="975" height="189" alt="image" src="https://github.com/user-attachments/assets/1729d0c2-f283-49dd-8fd0-7d6c870adf06" />

- Apply the Manifest:
To deploy the application, we apply the manifest files we created earlier. These files give Kubernetes templates for creating deployments and services resources for deployment and expose our application. 
<img width="975" height="164" alt="image" src="https://github.com/user-attachments/assets/b55714bb-e2c0-469c-9a80-9c60c70e6d60" />

---

✅ Summary

We launched an EC2 instance.

- Set up an EKS cluster with eksctl.

- Built a Docker image for our backend.

- Pushed it to Amazon ECR.

- Created Kubernetes manifests (Deployment + Service).

- Deployed and exposed the backend using kubectl.

  Our backend is now live on Kubernetes 🎉





