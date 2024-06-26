# kubernetes-setup-in-Jenkins

Minikube enables you to run a Kubernetes cluster locally on your machine.

Jenkins is an open-source automation tool for Continuous Integration (CI) and Continuous Deployment (CD).

Jenkins is installed on Linux(ubuntu) machine and minikube is running on Virtual Box VM.

Below Jenkins Plugins need to be installed:

Docker Version 1.2.9 — This plugin integrates Jenkins with Docker

Docker Pipeline Version 1.29 — Build and use Docker containers from pipelines.

Kubernetes plugin — This plugin integrates Jenkins with Kubernetes

1. kubectl apply -f account.yaml
2. kubectl describe secrets/jenkins-token
3. In Jenkins click on Manage Jenkins → Manage Credentials
   Secret: token string , Paste token data in a secret field
   create Kubernetes Id (my_kubernetes)with token data(token string )
![minikube-jenkins-1](https://github.com/bhaskarsaini27/kubernetes-setup-in-Jenkins/assets/103110177/8d5c3ce9-4e69-4824-a664-bee34823e79a)

4. Save DockerHub credentials in a Jenkins
   ![minikube-jenkins-2](https://github.com/bhaskarsaini27/kubernetes-setup-in-Jenkins/assets/103110177/40957950-9380-4730-b1ab-4a93e9806f77)

5. Configuring Kubernetes plugin

   Jenkins — manage Jenkins — Manage Nodes & Clouds

   Configure system scroll to bottom and in Add a new cloud, select Kubernetes

   Convert certificate info into base64 encoding and paste it in a field ( Kubernetes server certificate key)
   
   5a) cat $HOME/.minikube/ca.crt | base64 -w 0; echo
   
   5b) Use Kubernetes Id(my_kubernetes) which was created earlier and secret cert key , the output of last command.
   ![minikube-jenkins-3](https://github.com/bhaskarsaini27/kubernetes-setup-in-Jenkins/assets/103110177/1e8de5f2-0d17-4cda-8d73-42b396a13576)
   
   5c) setfacl -d -m u:jenkins:rwx $HOME/.minikube
   
   5d) setfacl -d -m g:jenkins:rwx $HOME/.minikube

