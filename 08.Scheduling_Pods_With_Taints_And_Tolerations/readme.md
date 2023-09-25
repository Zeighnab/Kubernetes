# Taints and Tolerations – Concepts

Taints and tolerations are a mechanism that allows you to ensure that pods are not placed on inappropriate nodes. Taints are added to nodes, while tolerations are defined in the pod specification. When you taint a node, it will repel all the pods except those that have a toleration for that taint. A node can have one or many taints associated with it.

For example, most Kubernetes distributions will automatically taint the master nodes so that one of the pods that manages the control plane is scheduled onto them and not any other data plane pods deployed by users. This ensures that the master nodes are dedicated to run control plane pods.

A taint can produce three possible effects:

* NoSchedule - The Kubernetes scheduler will only allow scheduling pods that have tolerations for the tainted nodes.

* PreferNoSchedule - The Kubernetes scheduler will try to avoid scheduling pods that don’t have tolerations for the tainted nodes.

* NoExecute - Kubernetes will evict the running pods from the nodes if the pods don’t have tolerations for the tainted nodes.

## Scenerio:

You have been given a three-node cluster. Within that cluster, you must perform the following tasks to taint the production node in order to repel work. You will create the necessary taint to properly label one of the nodes `prod`. Then you will deploy two pods — one to each environment. One pod spec will contain the toleration for the taint.

## Task:

* Taint one of the worker nodes to identify the prod environment.

* Create the YAML spec for a pod that will be scheduled to the dev environment.

* Create the YAML spec for a pod that will be scheduled to the prod environment.

* Deploy each pod to their respective environments.

* Verify each pod has been scheduled successfully to each environment.


![](./img/CKA-LABS_%20Scheduling%20Pods%20with%20Taints%20and%20Tolerations%20in%20Kubernetes.png)