# MERN Stack Application on AWS Three Tier Web Architecture 

## Description: 
This workshop is a hands-on walk through of a three-tier web architecture in AWS. I manually created the necessary network, security, app, and database components and configurations in order to run this architecture in an available and scalable manner.

### Tech Stack Used 
* React
* Nodejs
* MySQL
* AWS Services (VPC, EC2, RDS, S3, ELB, ASG, Cloudfront, IGW, NAT GW, Route53, ACM).  

## Pre-requisites:
1. An AWS account. If you don’t have an AWS account, follow the instructions [here](https://aws.amazon.com/console/) and
click on “Create an AWS Account” button in the top right corner to create one.
1. IDE or text editor of your choice.

## Architecture Overview
![Architecture Diagram](https://github.com/aws-samples/aws-three-tier-web-architecture-workshop/blob/main/application-code/web-tier/src/assets/3TierArch.png)

In this architecture, a public-facing Application Load Balancer forwards client traffic to our web tier EC2 instances. The web tier is running Nginx webservers that are configured to serve a React.js website and redirects our API calls to the application tier’s internal facing load balancer. The internal facing load balancer then forwards that traffic to the application tier, which is written in Node.js. The application tier manipulates data in an Aurora MySQL multi-AZ database and returns it to our web tier. Load balancing, health checks and autoscaling groups are created at each layer to maintain the availability of this architecture.

## Workshop Instructions:

See [AWS Three Tier Web Architecture](https://catalog.us-east-1.prod.workshops.aws/workshops/85cd2bb2-7f79-4e96-bdee-8078e469752a/en-US)




The frontend code is located in web-tier directory inside the application-code folder.

The backend code is located in app-tier directory inside the application-code folder.

## 🖥️ Installation of frontend

Note: You should have nodejs installed on your system. Node.js

👉 let install dependency to run react application

    cd application-code/web-tier
    npm install



## 🖥️ ️Installation of backend

Note: You should have nodejs installed on your system. Node.js

👉 let install dependency to run Nodejs API

    cd application-code/app-tier
    npm install

Now we need to create .env file that holds all the configuration details of the backend. you should be in backend directory

    vim DbConfig.js

add below content

    DB_HOST=localhost or URL_of_RDS
    DB_USERNAME=user_name_of_MySQL
    DB_PASSWORD=passwod_of_my_sql
    PORT=3306

