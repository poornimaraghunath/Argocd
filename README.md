 what is Gitops ?
 
 Gitops uses git as single source of truth to deliver the applications and infrastructure

 Why Gitops ?

 In CI process there was always a git as source of truth but in CD approach we used to use shell scripts or ansible for CD process but if any changes were made kubernetes cluster we are not able to identify them.So then the process of gitops came

 There are different types of Gitops  tools
  #Argocd
  #Flux
  #JenkinsX
  #Spinnaker

  # Principles of Gitops
    Declartive
    Versioned and immutable
    pulled automatically
    Continuoulsy reconciled - It does not allow any changes manually on kubernetes cluster

    Gitops controller will have inmemory cache which will read all the resorces deployed on cluster and stores in the inmemory cache and also it reads github manifest and even stores that if there any difference between git manifests and resource it will overwrite the change on kubernetes cluster

    For now the gitops controllers are targeted to only kubernetes

 # Advantages of Gitops
    Security
    Autohealing
    Versioning
    Auto upgrades
    Continuous reconcilation


# Argocd
  
  Created by Enginners at Apaltix
  It is open Source

  Gitops it always tries to maintain the synch(state) betweem git and kubernetes
  If someones tries to modify in cluster it will overwrite with whatover is present in git because git is always single source of truth.

  # Argocd Architecture
     It contains the below components

     Reposerver - it is one microservice which connects to git and get the state

     Application controller - It is another microservcie which connects to k8's and get the state

     It compares the synch between them if there is any differnece application controller synches with state of git.

     APi Server - Which is used by users to communicate to Argocd by using UI/CLI

     DEX - It is very lightweight OIDC it connect with any external identities which helps in sso.

     Redis - it is used for caching used as inmemory

     Application set controller -

     notifications controller -It is released in latest version of Argocd 

     #Argocd can be installed in three ways

       -Yaml manifests
       -Helm
       -operator


# Installation

First install #kubectl the command line tool to interact with kubernetes cluster
 # https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

Then install Docker is it dependency for minikube
# Run the below command to Install Docker

sudo apt update
sudo apt install docker.io
# Grant Ubuntu user permission to docker deamon.
sudo su - 
usermod -aG docker ubuntu(Ubuntu user will be added to docker group)
systemctl restart docker

# Then install minikube 
https://minikube.sigs.k8s.io/docs/start/

# Then install Argocd using Plain manifests
 https://argo-cd.readthedocs.io/en/stable/getting_started/

By default argocd comes in cluster Ip mode it means only it can be accessed in kubernetes cluster 

To access it from the laptop change it nodeport mode in argocd svc in argocd server component

After changing to nodeport mode it can be accessed from minikube cluster to access it from the browser we need to port forwarding 

Use the below command to do port forwarding  

# kubectl port-forward svc/argocd-server -n argocd --address 0.0.0.0 8080:443
Always run in that background

# How to get argocd UI password
 Kubectl get secret -n argocd

In  that go to argocd-initial-admin-secret
 # kubectl edit secret argocd-initial-admin-secret -n argocd
 Then copy the password from that and do decoding by using the below command

 UXVZa04xaWR3a1kyUHVjVg==

 Enter the below command to decode 

echo value of the secret /n | base64 --decode

#Follow this argocd repository for argocd examples
https://github.com/argoproj/argocd-example-apps

# How to use argocd CLI
    https://argo-cd.readthedocs.io/en/stable/cli_installation/

    Enter command argocd login 100.25.110.105:8080(ipaddress of the url)
    Then enter username and password
     

# Command to create the application through CLI 
 argocd app create guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path guestbook --dest-server https://kubernetes.default.svc --dest-namespace default

# Once application is deployed enter the below command to check the status
  argocd app get guestbook
 
# To sync the application and see the pods enter the below commnand
 argocd app sync guestbook
    
     
  









