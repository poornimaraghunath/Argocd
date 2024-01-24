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


