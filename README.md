# myways_task #

## Task Description ##

#### 1. Pick your favourite open source project on Github,
#### 2. Create a docker for this and push to ECR,
#### 3. Make a github repo for code you select and with docker file,
#### 4. Use AWS EC2 t2.micro for containers with ECS, create a task in ECS for this service to start the app,
#### 5. Use API Gateway and AWS Lambda to make an endpoint to start the app,
#### 6. Use Lambda to start the app and give output from ECS Task as output 


## Architecture Diagram ##
![picture alt](https://github.com/sheikhaafaq/myways_task/blob/master/diagrams/architectureDiagram.jpg "Architecture Diagram")


## Steps To Follow ##
### 1. Launch an EC2 Instance and configure:
  1. Docker `sudo yum install docker -y`
  2. awscli `sudo yum install awscli -y`


### 2. Create an ECR repository and also define an IAM Role, so that EC2 have permisions to login ECR.
  * At EC2, define a Dockerfile and create an image, then push the image to ECR
  * commands:
    1. `aws ecr get-login-password --region < region name > | docker login --username AWS --password-stdin < repo address > `
    2. `docker build -t <image> ./<imageworkspace>/ `
    3. `docker tag  <Image name:version>  <repo address/Image name:verison> `
    4. `docker push <repo address/Image name:version>`
  ### Image Details
  ![picture alt](https://github.com/sheikhaafaq/myways_task/blob/master/diagrams/imageDetails.jpg "Image Details")

  ### EC2 to ECR Role
  ![picture alt](https://github.com/sheikhaafaq/myways_task/blob/master/diagrams/EC2_ECR_Role.jpg "EC2 to ECR Role")
   

### 3. Create ECS Cluster on 2 Linux EC2 Instance with default settings.
  
  * Configure Cluster Template 
  ![picture alt](https://github.com/sheikhaafaq/myways_task/blob/master/diagrams/configureCluster.jpg "Configure Template")


  * Cluster Details
  ![picture alt](https://github.com/sheikhaafaq/myways_task/blob/master/diagrams/myCluster.jpg "Cluster Deatails")


  * Configure Task Definition
  ![picture alt](https://github.com/sheikhaafaq/myways_task/blob/master/diagrams/taskDefinition.jpg "Task Definition")


### 4. Create a Lambda Function and an IAM Role to execute the task.

  * Task Execution Function to run task
  ![picture alt](https://github.com/sheikhaafaq/myways_task/blob/master/diagrams/lambdaFunction.jpg "Task Exec Function")


  * IAM Role to Execute Task
   ![picture alt](https://github.com/sheikhaafaq/myways_task/blob/master/diagrams/taskExecRoles.jpg "Task Exec Roles")


### 5. Create an API Gateway to Trigger Lambda Function, so that Lambda Function should Execute Task.

  * API Gateway
   ![picture alt](https://github.com/sheikhaafaq/myways_task/blob/master/diagrams/apiGateway.jpg "API Gateway")


   * API Gateway OutPut when task gets Executed
    ![picture alt](https://github.com/sheikhaafaq/myways_task/blob/master/diagrams/apiOut.jpg "API Gateway OutPut")

### Hope you like it,
### Thank you
