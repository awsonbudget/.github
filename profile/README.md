# ~~AWS~~ K8S on Budget

## COMP 598 – Topics in Computer Science 01 - McGill University

Winter 2023 Topic: Cloud Computing

![amazing](https://raw.githubusercontent.com/awsonbudget/.github/main/profile/amazing.png)

## Overview

KOB is a simple Kubernetes-like cloud management system. There are 4 main components in this system.
- `manager`: This is a centralized, fault-tolerant cloud manager, that manages all the clusters in the system. All the cloud management request will be sent to the manager, and the manager will take care of the rest. Some example requests can be: to spin up a new server on a cluster, to enable dynamic scaling on a pod, to launch a job, and much more. Since this is the single point of failure in the entire system, it is made fault tolerant with etcd, allowing us to quickly recover in case of failure without losing any state information.
- `cluster`: Each virtual machine should have one cluster server running. The cluster server is the one that receives request from the centralized manager, and perform the requested action on the machine. A cluster can have multiple pods inside of it, and each pod can host a different application. Inside of each pod, there can be multiple instances of the same application running, and the load balander will balance the load across all the instances. If you enable dynamic scaling on a pod, then the pod will automatically add/remove instance based on resource usage.
- `dashboard`: A Web dashboard that provides a view of all the resources in the cloud system.
- `cli`: The CLI is used to issue commands to the cloud manager via a RESTful API.

## Setup

To get started, we first need to install a couple of dependencies.
- `docker`. In KOB, all servers are packaged as Docker containers.
- `etcd`. A distributed KV store that enables fault tolerance for our cloud manager.
- `haproxy`. Our load balancer to balance traffics to all server nodes in each cluster.
- `nginx`. We use it for demo purpose, it does not have to be Nginx.
- `python`. To run all the clusters and the cloud manager.
- `poetry`. To manage Python environment and dependencies.
- `go`. To build the CLI toolset.
- `nodejs`. To host the Web dashboard.
