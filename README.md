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
#image_1
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

#image_2
- Put jenkins-ec2-public-IP:8080 in the Browser and login the password

#image_3
# Configuring Jenkins Pipeline

- Installing suggusted Plugins and Creating user from the browser when loggin in

- Adding AWS credentials in secret text 

- Adding Github credentials with github-token

  **Dashboard > Manage Jenkins > Credentials > system > Global credentials (unrestricted) + Add Credentials**
  
#image_4  
  - Configure the pipeline using SCM and Build Triggers 

#image_5
#image_6
# Using Github Webhook to trigger jenkins

from repo"s settings adding webhoob with jenkins's

#image_7
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

#image_8
#image_9


# Accessing the app URL

#image_10
#image_11




# Checking the app liveness and readiness

#image_12



