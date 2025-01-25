<h1> Lab - 2 :- IaaS/PaaS architecture </h1>

1. Describe how this application can be deployed in the cloud using IaaS infrastructure.
 

DESCRIPTION :- Iaas supports to take different virtualized computing resources such as storage,servers and networks on rent. I will install,configure and maintain everything which includes OS and middleware over infrastructure. So in this deployment I will use Flask,React and Postgres on Virtual Machines according to the task. 

STEP BY STEP DEPLOYMENT :- 

(1) Infrastructure Setup :- Creation of VMs for each components :- (1) Flask - To run the backend application dedicated VM will be made for it which will act as an Web Server. (2) Postgres - Another creation will be done for the required storage with Database integrity. (3) React - Deploying React on another VM for the UI Frontend. --> Ensuring that all VMs are at the same dedicated Networks for better interactions between components.

(2) Network Setup :- 

(1) Setting up a load balancer which will distribute the traffic among flask instances if scaling is needed.

(2) Configuration of a security group and firewall rules will be done to allow access of some specific ports such as port80 for HTTP,port5432 for Postgres and so on.

(3) Storage Setup :- 

Attaching a determined storage volume example AWS EBS Persistent Disk to the postgres VM to make sure data do retain on the machine even if the VM gets restart.

2. Describe how this application can be deployed in the cloud using PaaS infrastructure.

DESCRIPTION :- Paas will provide us a managed platform for deploying our application without thinking much about the infrastructure and maintainance. The cloud provider helps us to handle hardware,OS and runtime environment which will allow us to focus on the deployment and development. 

STEP BY STEP DEPLOYMENT :- 

(1) Deploying flask Backend :- Using a Paas service such as AWS Elastic Beanstalk the deployment of flask application will take place. The AWS Elastic Beanstalk will help to complete task like load balancing,scaling and runtime configuring etc.

(2) Hosting React UI :- Here I will be using a static hosting service to deploy the React frontend such as AWS S3 with CloudFront for faster global delivery.

(3) Database Setup :- A fully managed database service such as AWS RDS for PostgreSQL will be used by me which will provide services such as scaling,backups and high availability.

3. For each case, draw a diagram that represents the target architecture and describe each of the chosen cloud components.
      
                                                        Internet 
                                                            |
                                                 -----------------------
                                                      Load balancing 
                                                            |
                                                -------------------------
                                                |                       |
                                             Flask VM              React UI VM
                                                |                       |
                                            Postgres VM 
