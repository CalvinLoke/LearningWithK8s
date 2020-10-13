# MicroK8s

MicroK8s is a light-weight version of Kubernetes, excellent for learning how Kuberentes works. I will be documenting some of the important commands and information regarding the use of Microk8s in this section. 

# Installing microk8s

## Pre-requisites
Ensure that your host system meets the following requirements:

- Ubuntu 20.04 LTS, 18.04 LTS or 16.04 LTS, or any OS that supports `snapd`
- At least 20 GB Disk Space
- At least 2 GB Memory

More information regarding the requirements can be found [here](https://microk8s.io/docs)

## Install from snap
`sudo snap install microk8s --classic`

## Adding the current user to gain admin rights
`sudo usermod -a -G microk8s $USER`

`sudo chown -f -R $USER ~/.kube`

`su - $USER`

## Checking if Microk8s is running
`microk8s status --wait-ready`

## Enabling add-ons 
As Microk8s is barebones, many of the services need to be enabled. They can be enabled using the `microk8s enable` command. 

`microk8s enable dns dashboard storage`

Similarly, you can disable it using

`microk8s disable dns dashboard storage`

# Kubernetes using Microk8s
Running Kubernetes on Microk8s is simply done by appending `kubectl` to the `microk8s` command. This also means that most, if not all of `kubectl` commands will work in the same manner. 

If you would like, you could alias `microk8s.kubectl`, assuming that you do not have `kubectl` currently installed on your host machine. 

` alias kubectl='microk8s kubectl' `

# Useful microk8s commands

Note that kubectl commands *should* work. 

## Enabling MetalLB LoadBalancer for the microk8s kubernetes cluster
`microk8s enable metallb`

`<IP-address range>-<IP-address range>`

## Getting all the namespaces
`microk8s kubectl get all --all-namespaces`

## Resetting the whole cluster
`microk8s.reset`

## Getting the status of microk8s 
`microk8s.status`

## Official kubectl cheat sheet

[Here is the link](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)


