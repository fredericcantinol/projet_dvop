# projet_dvop
## Objectives:

The objectives of this project exam are to ensure that you are able to build and maintain a DevOps environment, so you will be evaluated about the following themes:

 improve an existed application integration and deployment process
 implement automation as far as possible
 best practice when implementing CI/CD pipeline
DevSecOps : ensure that security is guaranty during CI/CD process
# 1- Context:

Remember the POZOS company, you had containerized a simple application for them (4DOKR TP Exam).

The DSI was so happy about your work and want you to manage the evolution of the deployment process.

The innovation department wants to disrupt (again) the existing infrastructure to ensure that the integration and deployment process are totally automated: DevOps culture.

POZOS wants you to build a POC to show how CI/CD pipeline can help you and how much this technology is efficient.

# 2- Infrastructure:

For this POC, you will only use 4 servers (on-premise) with the followings roles:

 deployment server: on this server, you will run Jenkins and all the deployment tools
 App server: on this server, you will deploy the student_list (Connexions vers un site externe.)
Registry: this server will hosted the private registry to push and pull image
Code Repository: this server will hosted a local gitlab to manage your source code
POZOS recommends you to use centos7.6 OS because it's the most used in the company.

Please also note that you are authorized to use a virtual machine base on Centos7.6 and not your physical machine.

The security is a very critical aspect of POZOS DSI so please do not disable the firewall or other security mechanisms otherwise please explain your reasons in your delivery.

# 3- Before starting:

Before starting the pipeline, make sure you complete Dockerfile and docker-compose.yml (currently both are empty)

So ensure that your docker-compose up -d deploy the application as expected

After that, you are ready to start building pipeline

# 04- Pipeline component integration and build: 12 Points

POZOS will give you some recommendations about the tools you must consider when building your pipeline.

The following step is needed:

**Step 1:** When code is pushed on code repository the pipeline must be started

**Step 2:** Code repository must inform the building system to run pipeline through webhook

**Step 3:** Build system must get the code from the code repository

**Step 4:** Build system must build the docker image from simple_api Dockerfile

**Step 5:** Build system must test the image (integration system)

**Step 5.1:** run a container with the builded image

**Step 5.2:** test if the simple_api is working as expected (curl -u toto:python -X GET http://:<host IP><API exposed port>/pozos/api/v1.0/get_student_ages)

**Step 6:** Build system must validate the image with the scanner image tools

**Step 7:** Build system must push the image on the private docker image registry

**Step 8:** Build system must deploy the application on Application using a deployment tool

**Step 9:** Build system must run the security test to ensure the application is secure (E2E Tests)

Source Code + Version Control: You may publish your code on your on-promise gitlab (Connexions vers un site externe.)
Build System and Build Tool: Jenkins is the recommended tools (with the necessary plugins), you are allowed to use the same Jenkins (Connexions vers un site externe.) docker image used as part of the 4DVOP course 
Integration System: docker and curl command
Docker image scanner: Clair
Docker image registry: docker private registry (https://hub.docker.com/_/registry)
Deployment tool: You will use your favorite tools (puppet, chef and Ansible), POZOS recommend you Ansible
E2E tests: Gautlt with Arachni

# 05- Pipeline component monitoring: 3 points

POZOS needs you to implement some monitoring solution on different level

 System monitoring: use DataDog to monitor your infrastructure
 Software metrics: use DataDog to monitor docker daemon
 Log monitoring: use Splunk to monitor docker container log
 
# 06- BONUS STAGE: 5 points

Go Further

Now, manually create a job and related step, but if you lose your Jenkins server, you will be obliged to create all the steps again.

To prevent it, you can use a jenkinsfile (https://jenkins.io/doc/book/pipeline/jenkinsfile/) to define your pipeline.

So you must write a Jenkins file to code your pipeline rather than creating out through interface.

This is our bonus stage :-)

# 07- Delivery: 5 points

This project should be realized in a group of 3 students maximum per group .

Plagiarism and copying are strictly forbidden.  Any elements of the kind will be scored to 0 grade and cheater status for all people implicated in the fraud.

Your delivery must be zip named <IDBOOSTER_member1>_<IDBOOSTER_member2>_<IDBOOSTER_member3>.zip that contain:

a doc or PDF file with your screenshots (of each build step on Jenkins) and explanations of your work.
Your repository code with
The app file (Dockerfile, docker-compose.yml)
ansible, chef or puppet playbook
Your work will be evaluated on:

Explanations quality
Screenshots quality (relevance, visibility)
Oral Presentation quality
-----------------------------------------------------------
## 4DOKR

# Objectives

The objectives of this practice exam are to ensure that you are able to manage a docker infrastructure, so you will be evaluated about the following

themes:

- improve an existed application deployment process
- versioning your infrastructure release
- address best practice when implementing docker infrastructure
- Infrastructure As Code

# Context

POZOS is an IT company located in France and develops software for High School.

The innovation department want to disrupt the existing infrastructure to ensure that

it can be scalable, easily deployed with a maximum of automation.

POZOS wants you to build a POC to show how docker can help you and how much this technology is efficient.

For this POC, POZOS will give you an application and want you to build a "decouple" infrastructure based on Docker.

Currently, the application is running on a single server with any scalability and any high availability.

When POZOS needs to deploy a new release, every time some goes wrong.

In conclusion, POZOS needs agility on its software farm.


# Infrastructure

For this POC, you will only use one single machine with a docker installed on it.

The build and the deployment will be made on this machine.

POZOS recommends you to use centos7.6 OS because it's the most used in the company.

Please also note that you are authorized to use a virtual machine base on Centos7.6 and not your physical machine.

The security is a very critical aspect of POZOS DSI so please do not disable the firewall or other security mechanisms otherwise please explain your reasons in your delivery.

# Application Architecture

The application that you will be working on is named "student_list", this application is very basic and enables POZOS to show the list of the student with their age.

student_list has two modules:

the first module is a REST API (with basic authentication needed) who send the desire list of the student based on JSON file
The second module is a web app written in HTML + PHP who enable end-user to get a list of students
Your work is to build one container for each module an make them interact with each other

Application source code can be found here (Connexions vers un site externe.)

The files that you must provide (in your delivery) are **Dockerfile** and **docker-compose.yml** (currently both are empty)

Now it is time to explain you each file's role:

 docker-compose.yml: to launch the application (API and web app)
Dockerfile: the file that will be used to build the API image (details will be given)
student_age.json: contain student name with age on JSON format
student_age.py: contains the source code of the API in python
index.php: PHP  page where end-user will be connected to interact with the service to list students with age. You need to update the following line before running the website container to make **api_ip_or_name** and **port** fit your deployment
```
$url = 'http://<api_ip_or_name:port>/pozos/api/v1.0/get_student_ages';
```

# Build and test (7 points)

 
POZOS will give you information to build the API container

Base image
To build API image you must use "python:2.7-stretch"

Maintainer
Please don't forget to specify the maintainer information

Add the source code
You need to copy the source code of the API in the container at the root "/" path

Prerequisite
The API is using FLASK engine,  here is a list of the package you need to install

```
apt-get update -y && apt-get install python-dev python3-dev libsasl2-dev python-dev libldap2-dev libssl-dev -y

pip install flask flask_httpauth flask_simpleldap python-dotenv
```
Persistent data (volume)
Create data folder at the root "/" where data will be stored and declare it as a volume

You will use this folder to mount student list

API Port
To interact with this API expose 5000 port

CMD
When container start, it must run the student_age.py (copied at step 4), so it should be something like

```
CMD [ "python", "./student_age.py" ]
```
Build your image and try to run it (don't forget to mount student_age.json file at /data/student_age.json in the container), check logs and verify that the container is listening and is  ready to answer

Run this command to make sure that the API correctly responding (take a screenshot for delivery purpose)
```
curl -u toto:python -X GET http://:<hostConnexions vers un site externe. IP><API exposed port>/pozos/api/v1.0/get_student_ages
```
**Congratulation! Now you are ready for the next step (docker-compose.yml)**
 
# Infrastructure As Code (5 points)

After testing your API image, you need to put all together and deploy it, using docker-compose.

The **docker-compose.yml** file will deploy two services :

 website: the end-user interface with the following characteristics
image: php:apache
 environment: you will provide the USERNAME and PASSWORD to enable the web app to access the API through authentication
volumes: to avoid php:apache image run with the default website, we will bind the website given by POZOS to use. You must have something like
```
./website:/var/www/html
```
depend on: you need to make sure that the API will start first before the website
port: do not forget to expose the port
API: **the image builded before** should be used with the following specification
image: the name of the image builded previously
 volumes: You will mount student_age.json file in /data/student_age.json
port: don't forget to expose the port
Delete your previous created container

Run your docker-compose.yml

Finally, reach your website and click on the bouton "List Student"

If the list of the student appears, you are successfully dockerizing the POZOS application! Congratulation (make a screenshot)

# Docker Registry (4 points)

POZOS need you to deploy a private registry and store the built images

So you need to deploy :

a docker registry (Connexions vers un site externe.)
a web interface (Connexions vers un site externe.) to see the pushed image as a container
Or you can use Portus (Connexions vers un site externe.) to run both

Don't forget to push your image on your private registry and show them in your delivery.

# Delivery (4 points)

This exam must be realized:

By your own
Without internet
Without you courses
Plagiarism and copying are strictly forbidden.  Any elements of the kind will be scored to 0 grade and cheater status for all people implicated in the fraud.

Your delivery must be zip named IDBOOSTER.zip (replace IDBooster by your own) that contain:

A doc or PDF file with your screenshots and explanations.
Configuration files used to realize the graded exercise (docker-compose.yml and Dockerfile).
Your delivery will be evaluated on:

Explanations quality
Screenshots quality (relevance, visibility)
Presentation quality
