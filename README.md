# Serverless Rest API Architecture

![Serverless](https://raw.githubusercontent.com/Assassin010/SpringBoot-Serverless-Api-G/main/Serverless.drawio.png)

**1. Introduction**

Let's discuss the benefits of using AWS Lambda and Spring Boot 3 before we begin. You're probably accustomed to packaging your programmes as JAR files and distributing them to servers. You might even deploy the application to Kubernetes in a containerised form using Docker.

Scalability, security, and patching are all important considerations when managing your own server. You must take into account the volume of traffic your application will experience when you deploy it to a server. You might need to scale up to accommodate the traffic if your server is running at 100 percent of its capacity  

If your server is only being used 10% utilization, you might consider scaling down to save money.

AWS Lambda is a serverless compute solution that allows you to run code without the need for server provisioning or management. You only pay for the compute time you use. This indicates that my own project, which will not receive a lot of traffic, is a great choice for AWS Lambda. This use case is ideal for applications with variable traffic or that can scale to zero.


Most people are familiar with this concept when it comes to deploying functions as a service (FaaS), however in this article we will deploy a whole Spring Boot REST API. According to the AWS Pricing Page, the free tier of AWS Lambda includes one million free requests per month and 400,000 GB-seconds of computing time each month. This means that for the majority of the side projects I'm working on, I can deploy them to AWS Lambda for free.


**2. Prerequisites**

- Read the Quick Start here: https://github.com/awslabs/aws-serverless-java-container/wiki/Quick-start---Spring-Boot3
Thanks to Mark Sailes for all of his help with this tuto

- Java 17
- Spring Boot 3.1
- AWS CLI
- AWS SAM CLI
- GIT


**3. Agenda**

In this article, you will build a new Spring Boot 3 application, as well as a CRUD REST API, which you will package and deploy to AWS Lambda.

- start.spring.io
spring boot 3.1.0
maven / java
web, webflux

- Build CRUD REST API
post package
Post Record
PostNotFoundException
PostController

- Blog Posts Loader
JsonPlaceholderService

- Test locally using http client before packaging for production


**4. Maven Model**

The Maven Archetype is a project template that you can use to create new projects. The AWS Serverless Spring Boot 3 Archetype is a Maven project that you can use to create a new Spring Boot 3 project that includes an AWS Serverless container for Spring Boot 3. This will also create the exact Maven configuration needed. needed to create an AWS Lambda deployment package. If you are using IntelliJ IDEA, you can use the Maven Archetype to generate a new project but you can also use Spring Initializr. `aws-serverless-springboot3-archetype`

If Maven is already installed, you can use the following command to create a new project:  

```
mvn archetype:generate -DgroupId=my.service -DartifactId=my-service -Dversion=1.0-SNAPSHOT \
       -DarchetypeGroupId=com.amazonaws.serverless.archetypes \
       -DarchetypeArtifactId=aws-serverless-springboot3-archetype \
       -DarchetypeVersion=2.0.0-M1

```


**5. AWS Resources**

To deploy your application to AWS Lambda, you must first create the AWS resources listed below.

- AWS Lambda
- API Gateway

You can create the resources manually using the AWS Console, or you can use code. In this Article you will use the AWS Console, but I have included some resources if you want to learn more about SAM and CDK.

**AWS SAM**

SAM stands for **Serverless Application Model**. It's an open-source framework for creating serverless applications on AWS. It simplifies the definition of AWS resources (infrastructure as code) required to run your application. It also includes a command line interface (CLI) for packaging and deploying your application to AWS.


SAM defines your application using a template file (`template.yaml`). The AWS resources required to run your application are defined in the template file. You should go over that template file and review it before deploying your application.

`mvn clean package sam deploy --guided`

**AWS CDK**

CDK stands for **Cloud Development Kit** 
AWS CDK is an open source software development framework that allows you to define the resources of your cloud application using familiar programming languages. Because the AWS CDK allows you to define your infrastructure in standard programming languages, you can write automated unit tests for your infrastructure code in the same way that you do for your application code.
