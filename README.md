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
