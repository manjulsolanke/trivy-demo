# Trivy
## Installation 
### Ubunut
  ```bash 
sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
 ```
 OR 

The process above can be automated by the following script:

 ```bash 
  sudo -i
  curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin v0.38.0
  ```
 
 
 ### MacOS
   ```bash
   brew install trivy
   ````
   
## Container Image
Trivy supports two targets for container images.

Files inside container images

Container image metadata

### Files inside container images

Vulnerabilities

Misconfigurations

Secrets

Licenses

###  Vulnerabilities
  
  ```bash
  
  trivy image python:3.4-alpine # By default, vulnerability and secret scanning are enabled.
  
  trivy image --scanners config python:3.4-alpine # configuration check 
  
  trivy image --scanners license python:3.4-alpine # license check
  
  trivy image --scanners secret python:3.4-alpine # secret check
  
  trivy image --vuln-type os   --severity CRITICAL python:3.4-alpine
  
  
  ```
  
 ### Filesystem
 
 ```bash
 trivy fs <path>
 ```
 
 ### Git Repository
 
 ```bash 
 trivy repo [YOUR_REPO_URL]
 trivy repo --branch <branch-name> <repo-name>
 trivy repo --commit <commit-hash> <repo-name>
 trivy repo --tag <tag-name> <repo-name>
 ```
  
  
### Tar Files

```bash
docker pull python:3.4-alpine
docker save python:3.4-alpine -o python:3.4-alpine.tar
trivy image --input python:3.4-alpine.tar
   ```
  
  
### k8s 

```bash
trivy k8s cluster --report summary # full cluster scan
trivy k8s --namespace=kube-system --report=summary deploy,configmaps
trivy k8s deployment <deployment-name> # Only deployment scan
trivy k8s --report=summary deployment,configmaps
```
  
### AWS

```bash
trivy aws --region us-east-1
trivy aws --service s3
trivy aws --service s3 --service ec2 # --service s3,ec2 works too
trivy aws --service s3 --arn arn:aws:s3:::example-bucket
```
