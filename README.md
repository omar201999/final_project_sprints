# MySQL-and-Flask

Mysql and Flask app deployed on AWS using  EKs Cluster using ECR private repositary, using terraform and ansible to provision the infastrusture and configure the EC2 to be configured as Jenkins Master and deploying eth app, 
Deployed the App through jenkins pipeline by
- bulding mysql and flask images.
- pushing images to ECr repositaries. 
- apply k8s mainfest.
- Triggering jenkins pipleline using github-webhook

# AWS Infrastructure 

- using default VPC 
- EKS with 2 worker nodes
- 2 private REPO ECR
- EC2 with SG and IAM role to allow jenkins deploying on ECR and EKS

# Kubernetes Mainfest

- Deployment for flask-app image with readiness and liveness
- ConfigMap for flask-app variables (deployment)
- ClusterIP service selects the deployment's pod
- Statefulset for mysql image with (pv and pvs)
- ConfigMap for mysql variables (statefulset)
- ClusterIP service selects the statefulset's pod
- Ingress using nginx-controller

# Convert the app into dockerized application


Building Flask image and mysql image with database table

run 
```
docker-compose up --build
```
to test the app locally put the url in the Browser
```
localhost:5002
```
![1](https://github.com/omar201999/final_project_sprints/assets/46471716/aedaf471-cca8-4144-8fbb-866e581b38ba)

# Configuring the EC2 with Ansible

- Configure jenkins
- Installing kubectl
- Installing AWSCli

# Applying Terraform and Ansible (IAC)

- using Bash Script to apply Terraform and Ansible 

```
sudo chmod +x bash.sh
```

- Ansible will appear msg with jenkins password

  ![2](https://github.com/omar201999/final_project_sprints/assets/46471716/ab316a49-88ea-4b81-a098-dbed1aa20831)


- Put jenkins-ec2-public-IP:8080 in the Browser and login the password


![3](https://github.com/omar201999/final_project_sprints/assets/46471716/35b3af3e-19ca-4ab4-a97a-fd45d180629f)

# Configuring Jenkins Pipeline

- Installing suggusted Plugins and Creating user from the browser when loggin in

- Adding AWS credentials in secret text 

- Adding Github credentials with github-token

  **Dashboard > Manage Jenkins > Credentials > system > Global credentials (unrestricted) + Add Credentials**
  
![4](https://github.com/omar201999/final_project_sprints/assets/46471716/3ca7a482-31e1-49e2-848e-2b0ca555be25)

  - Configure the pipeline using SCM and Build Triggers 
![5](https://github.com/omar201999/final_project_sprints/assets/46471716/cb592319-c038-46de-aed2-e79dea42ceb8)
![6](https://github.com/omar201999/final_project_sprints/assets/46471716/85b04b20-22e3-4071-963e-e087bc4fb3b2)

# Using Github Webhook to trigger jenkins

from repo"s settings adding webhoob with jenkins's

![7](https://github.com/omar201999/final_project_sprints/assets/46471716/39d6fc7c-c317-4ce6-be56-bd4e52cd52e4)

# Commit to the repo by uploading Jenkinisfile

the pipeline will be triggered and Build
jenkinsfile stages
- Build images (flask and mysql)
- Login to ECR
- Push images to ECR
- Get kubeconfig
- Installing nginx-controller for AWS
- Apply K8S Mainfest
- Output the App URL in the console output
![8](https://github.com/omar201999/final_project_sprints/assets/46471716/50440030-adb0-4e14-8630-c43a117a168f)
![9](https://github.com/omar201999/final_project_sprints/assets/46471716/567225e9-b3f2-447c-82c9-305bd3c38151)


# Accessing the app URL
![10](https://github.com/omar201999/final_project_sprints/assets/46471716/4b56f9a1-81e8-4e5c-9b0a-e50c5f7a0783)





# Checking the app liveness and readiness
![11](https://github.com/omar201999/final_project_sprints/assets/46471716/06df8f19-9923-40ed-893e-6018d0f68fce)




