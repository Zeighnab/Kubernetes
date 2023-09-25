## Scenerio:

You have been given a 3-node cluster. Within that cluster, you must deploy your application and then successfully update the application to a new version without causing any downtime. 
You will use the image linuxacademycontent/kubeserve:v1, which will serve as your application. 
You must perform the steps to verify your app successfully rolled out initially; create a service for your deployment, so it can be used by the end user; and then perform the update, verifying that the update did not experience any service interruption for your end users. 

## Task:

* Create and roll out a deployment, and verify the deployment was successful.

* Verify the application is using the correct version.

* Scale up your application to create high availability.

* Create a service from your deployment, so users can access your application.

* Perform a rolling update to version 2 of the application.

* Verify the app is now at version 2 and there was no downtime to end users.

![](./img/CKA-LABS_%20Performing%20a%20Rolling%20Update%20of%20an%20Application%20in%20Kubernetes.png)