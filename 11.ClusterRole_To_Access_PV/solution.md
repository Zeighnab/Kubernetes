1. SSH into the server provided

2. View the Persistent Volume within the cluster
```
kubectl get pv
```

3. Create a ClusterRole
```
kubectl create clusterrole pv-reader --verb=get,list --resource=persistentvolumes

kubectl get clusterrole
```

* Note: `pv-reader`(name of the clusterrole), `--verb`(action to perform) `--resource`(resources you want to access)

4. Create a ClusterRoleBinding
```
kubectl create clusterrolebinding pv-test --clusterrole=pv-reader --serviceaccount=web:default

kubectl get clusterrolebinding
```

* Note: `pv-test`(name of the clusterrolebinding), `--clusterrole`(the clusterrole you want to bind to), `--serviceaccount`(namespace of the pv)


5. Create a Pod to Access the PV
```
vim curlpod.yaml

kubectl apply -f curlpod.yaml

kubectl get pod -n web
```

* Note: The pod must be in the same namespace with the PV

6. Request Access to the PV from the Pod

* Open a new shell to the pod
```
kubectl exec -it curlpod -n web -- sh
```

* Curl the PV resource
```
curl localhost:8001/api/v1/persistentvolumes
```
