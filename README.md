REA Systems Engineer practical task
===================================

Introduction
============
While I am familiar with the concept of using orchestration for server and application deployments, unfortunately previous work experiences have not necessitated the need for me to focus my efforts on learning and using these tools. This absence of hands on experience has presented a challenge for me and limited how I approach this challenge in the available time frame.

I began by attempting to run the application locally which was a straightforward exercise. Next, knowing that REA Group has a heavy investment in AWS, I created an AWS account and began investigating how to deploy a Ruby Sinatra application in AWS. For an already AWS shop and an application workload that is suited to the cloud I focused my efforts on AWS Elastic Beanstalk and AWS CloudFormation rather than on-premises orchestration tools. AWS Elastic Beanstalk produced quick results having the application deployed and accessible with little effort. Understanding that AWS Elastic Beanstalk produces an AWS CloudFormation template I reviewed this template with the intention of developing enough of an understanding to create a deployable template. While not an effective approach to learning AWS CloudFormation, I choose this path due to the limited time frame and lack of previous exposure.

I am presenting the two approaches below. The first utilises AWS Elastic Beanstalk, which while the orchestration logic has effectively been provided for you, is an extremely simple and effective approach to deliver the required outcome. The second approach describes a process overview to consider when deploying this application via orchestration or otherwise, as the first approach doesn't demonstrate this understanding.


Approach 1 - AWS Elastic Beanstalk
==================================
Execution Instructions
======================
- Launch https://ap-southeast-2.console.aws.amazon.com/elasticbeanstalk/home?region=ap-southeast-2#/gettingStarted
- Specify application name: rea-simple-sinatra-app
- Choose Platform: Ruby
- Upload Simple Sinatra app source code
- Choose Create application
- Once complete the URL will be available from the application environment dashboard.

Requirements
============
- AWS account
- Simple Sinatra app source code

Assumptions and Design Choices
==============================
Assumptions
-----------
- AWS is trusted with maintaining the overall security of their cloud infrastructure.
- AWS Elastic Beanstalk provisions all resources in a secure manner.

Design Choices
--------------
- An AWS based solution leverages the investment REA Group has already made in the platform.
- This solution is chosen for its simplicity, ease of deployment, and idempotency.
- Cloud based orchestration provides tooling that is natively integrated across the platform.
- Removes maintenance overhead and complexity of integrating on-premises tooling.

Limitations
===========
- The simplicity and ease of deployment of this solution can result in cloud infrastructure and applications being deployed with little knowledge and/or understanding of the solution architecture. A thorough understanding is required to effectively assess the security of and support the solution.
- As cloud capabilities and service offerings are continually evolving it may be difficult to ensure that configuration-as-code can be applied with the same result in the future. By contrast, a customer with on-premises tooling can control the pace at which their environment changes.


Approach 2 - Process Overview
=============================
Execution Instructions
======================
- Deploy and configure guest VM, applying server OS from published VM templates. Templates should be used as to ensure that only approved operating systems are deployed.
- Apply required security patches and updates to OS and supporting components. Source OS image would ideally be pre-hardened and patched to limit exposure window where the system is vulnerable.
- Secure user access to VM through the creation and application of centrally managed resource and role security groups.
- Deploy and configure Ruby server from DML.
- Deploy simple-sinatra-app application source code from DML.
- Configure local host firewall to allow TCP port 80 ingress.
- Configure public or private DNS A record depending on the scope of access required.
- Execute tests to validate that web server responds appropriately on TCP port 80 and that the OS is secured to an accepted baseline.
- Update CMDB with any newly created configuration items.

Requirements
============
Approach provides a universal process overview therefore no specific requirements have been provided.

Assumptions and Design Choices
==============================
Assumptions
-----------
- Virtual machine host environment is configured with the required compute, networking and storage requirements to freely provision guest virtual machines. This is more relevant to on-premises virtualisation than cloud-based IaaS.
- Application is deployed to traditional VM hosts rather than modern alternatives such as containers or serverless computing.
- Local host firewall is enabled by default applying pre-determined defaults.

Design Choices
--------------
- Process overview can be applied irrespective of deployment method as the process applies to both manual and orchestrated deployment.
- Security policies are centrally applied to server OS through group policy or similar.
- All source media should be maintained as configuration items in a CMDB and be stored in a definitive media library (DML) of approved versions.
- Before use all media should be verified against a known hash value for the configuration item to ensure integrity and that the version is approved.

Limitations
===========
- I acknowledge that this approach does not fulfil the brief of providing a script and/or configuration to provision a new server and deploy the application. With sufficient knowledge and experience with orchestration tooling I believe the process overview provided would provide a suitable foundation to build out the required script and/or configuration.