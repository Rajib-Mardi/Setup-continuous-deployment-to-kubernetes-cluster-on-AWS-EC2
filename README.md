### Project:
* CD - Deploy to EKS cluster from Jenkins Pipeline 
### Technologiesused: 
* Kubernetes, Jenkins, AWS EKS, Docker, Linux 
### Project Description:

### Install kubectl inside Jenkins Container as root user


<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/6f8569d8-aa8c-403a-aa63-9ed135a320dd" width="700">

### Install aws-iam-authenticator inside Jenkins Container
* download the aws-iam-authenticatior
* edit execute perrmisssion
* move the file to usr/local/bin
* execute the command using ```aws-iam-authenticator help```



<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/05d434bc-885f-4f25-9d1a-d8b67aeb6c11" width="700">



<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/950e9368-4511-46fc-b2cb-92412ca92994" width="700">
### Create kubeconfig file to connect to EKS cluster and add it on Jenkins server

* Make a configuration file in the digital ocean sublets 
* create config file command ```vim config``` in digitalOcean server as we can see in fig
* values we need to update
   * 1.  server endpoint - The Kubernetes API server is the "public endpoint" for taking a cluster.
   * 2. certificate-authority-data - The certificate authority info can be found locally in ```cat .kube/config ```
   * 3. cluster name




<img src="(https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/e473e0a6-e962-4d2f-88d2-3a2f864c55f6" width="700">

####  copy it to the Jenkins container server.

* enter the Jenkins container as the user
* do ```cd ~ ``` then navigate to the home directory
* create .kube inside the jenkins home folder
* using docker copy command ``` docker cp config container id:var/jenkins_home/.kube/ ``` we can easily copy  the file



<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/99c4d885-fb15-4521-b389-31f8c0872214" width="700">


<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/ebe21fd3-cdeb-442f-8330-747641f00559" width="700">

* We can see that the kubeconfig file has been copied into Jenkins' home directory using the command ``` cat .kube/config  ```

### Add AWS credentials on Jenkins for AWS account authentication


<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/68febc48-2c42-469d-9512-e74c61da18d8" width="700">

### Adjust Jenkinsfile to configure EKS cluster deployment 

* In the deploy stage, we are going to execute the shell command "kubectl create deployment, name of deployment, and image name."
* We are going to create a simple "nginx deployment."

* Inside the environment variable, set the access key ID and access secret key credentials.



 <img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/3b22d3f7-9fa8-4122-bc88-699455388ed2" width="700">
 
  * In the next step, add the commit and push the Jenkinsfile repository to remote repository.
* run the pipline in jenkins
* When we run the pipeline in Jenkins, we can see that the pipeline was successfully executed and that the logs for deployment were created.



<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/2004f8c5-05a1-4c6e-891f-cb0dac7ba6d1" width="700">



<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/755d39ef-8998-411f-9de2-451b5f8e7d64" width="700">

* In cluster, the  pods is  running..




<img src="https://github.com/Rajib-Mardi/Kubernetes-on-AWS-EKS/assets/96679708/79143a2d-830b-4900-8959-6311380e6fc3" width="700">

-----------------------------------------------------------------------

