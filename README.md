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
  
  
