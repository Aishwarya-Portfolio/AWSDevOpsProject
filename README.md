# AWSDevOpsProject
Deployment of Nginx webpage in EC2 instance using AWS DevOps.

#### **Tools Used -->**
1. Source Code Repository - Code Commit
2. Build - Code Build
3. Deploy - Code Deploy
4. CI/CD - Code Pipeline
5. Access management - IAM
6. Artifact Storage - S3
7. Deployed to - EC2 instance (Ubuntu)
8. Webserver - Nginx

![image](https://user-images.githubusercontent.com/91592578/228168560-65a324fc-a2db-4d80-b6b1-c3f8a823cf50.png)

### **Pipeline Flow -->**
* Develop
1. IAM user who has access to the Code commit makes changes to the code in local git repo which is cloned from Code Commit, and pushes it to the remote side.
2. This commit will trigger the Code Pipeline.
* Build
3. Which will first checkout the code from repo and will download it in agent's workspace.
4. Code build will read the buildspec.yaml file and the artifact will be build by follwing the steps mentioned in the yaml file.
5. Code build will generate the Artifact and store it in S3 bucket.
6. Code Build has a service role which gives it access to code commit for downloadng the source code and full access to S3 bucket to store the Artifact.
* Deploy
7. Code deploy will now take the artifact from S3 bucket.
8. It will read the steps mentioned in appspec.yaml file to install and configure nginx in the EC2 instance where we are deploying our webpage.
9. The artifact is deployed at the correct location inside the EC2 instance and the nginx service has been started by the code deploy agent.
10. The webpage will be accessible on the Public IP of the EC2 instance.
11. Here code deploy needs a service role to access - EC2, S3, Code Deploy.
12. EC2 also needs a service role to access - Code Deploy, EC2.
13. Code Pipeline needs a service role to access - Code Pipeline.

![image](https://user-images.githubusercontent.com/91592578/228171203-58864ce0-4a39-433b-b5ac-e4d50ec5b640.png)
