# LearningWithK8s

Documenting my process of learning Kubernetes

# Kubernetes Helpsheet

Similar to my LearningWithDocker repository, this `readme` file serves as a quick reference for the different commands that I have used. They are complied from multiple tutorials and documentation from the Kubernetes site or its variations. 

## Installing Kubernetes

<To be included later>

# Kubectl cheat sheet

[This](https://kubernetes.io/docs/reference/kubectl/cheatsheet/) serves as an excellent cheat sheet for all the specialized commands that are not listed in this documentation. 

# Important Kubernetes commands
This section will contain important commands that are commonly used during development. I have extracted them from various sources inlcuding from the cheat sheet that I have included in the earlier section. 

## Applying a manifest/yaml file to the kubernetes cluster
`kubectl apply -f <yaml-file-name>`

`kubectl apply -f <path-of-yaml-file>`

## Exposing a deployment
`kubectl expose deployment <deployment-name> --type=<service-type> --name<my-service-name>`

## Getting the status of currently running pods
`kubectl get pods`

## Getting the status of all current services, pods and deployments 
`kubectl get all --all-namespaces`

## Checking the logs of a particular pod/service/deployment
`kubectl describe <pod/service/deployment> <pod-name/service-name/deployment-name>`

`kubectl describe pod/<pod-name>`

`kubetcl describe service/<service-name>`

`kubectl describe deployment/<deployment-name>`

## Deleting pods/services/deployments
`kubectl delete <pod/service/deployment> <pod-name/service-name/deployment-name>`

`kubectl delete pod/<pod-name>`

`kubectl delete service/<service-name>`

`kubectl delete deployment/<deployment-name>`

`kubectl delete pods/services/deployments --all`

## Exec into the container/pod
`kubectl exec -it <pod-name> bash`


