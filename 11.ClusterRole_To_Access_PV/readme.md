## Scenerio:

Access the Kubernetes cluster within this lab environment. Within the cluster, a Persistent Volume (PV) has already been provisioned. You will need to make sure you can access the PV directly from a pod within your cluster. Create a pod with two containers in order to do so.

* The first container, using the image `curlimages/curl`, will allow you to use curl to directly access the Kubernetes REST API.

* The second container, using the image `linuxacademycontent/kubectl-proxy`, will allow you to create a proxy between the container and the Kubernetes API Server. Ensure this pod is created in the same namespace as the PV.

* By default, pods cannot access PVs directly, so you will need to create a `ClusterRole` and test the access after it's been created. 

* Every ClusterRole requires a `ClusterRoleBinding` to bind the role to a user, service account, or group. After you have created the ClusterRole and ClusterRoleBinding, try to access the PV directly from a pod.

![](./img/CKA-LABS_%20Creating%20a%20ClusterRole%20to%20access%20a%20PV%20in%20Kubernetes.png)