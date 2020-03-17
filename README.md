# Playing Drone and Gitea on local with k3d(k3s)

### Run full ci cd solution on kubernetes in local box for fun ?

**What we going to build?**

* A tiny k8s cluster by k3s
* A tiny git repo system by gitea (installed by helm)
* A tiny ci cd system by drone (installed by helm)

**They are all golang!**

* quick start,restart,install,upgrade. all in a few seconds
* easy understand prototype CICD
* easy play k8s cluster (API compatible , not really k8, k3 instead :blush:)


### Understand the tweak

Before I walk through steps in [INSTALL.md](./INSTALL.md), let 's understand it.

* Use k3d to launch k3s , 1 server + 2 workers for example, so the whole k3s cluster running on 3 docker containers.

* Once we get k3s cluster up which takes 5,6 secs (thanks to k3d :yum:) we install gitea and drone through its helm charts

* External access is through traefik ingress, here we need create kubernetes ingress for both drone and gitea,and local hosts file as local box DNS resolve

* Internal connection between drone and gitea (for oauth purpose) is through kubernetes service.

* We need to use consistent name for both ingress and kubernetes service , as the server name configured for gitea and drone will be mixed used by webhook,oauth and external access

**About the charts**

I use official chart for drone and k8s-land chart(3rd party) I found in github for gitea, however to get all work in k3s I have to create additional ingress as well as service to get above requirement meet.



### [Install steps](./INSTALL.md)
