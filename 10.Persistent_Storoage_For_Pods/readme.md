## Scenerio:

You have been given access to a two-node cluster. Your objective is to create persistent storage for the pod, and prove that the data resides on disk, even when you delete the pod. You must first create a PersistentVolume object in Kubernetes. Once the PersistentVolume has been created, you must create a PersistentVolumeClaim in order for you to claim that volume for the pod. Once you have your PersistentVolume and PersistentVolumeClaim, you are now ready to create the pod.

## Tasks:

* Create a PersistentVolume named `redis-pv` with `1Gi` of storage and `ReadWriteOnce` access mode. Mount the PersistentVolume to the `/mnt/data` directory on the host machine.

* Create a PersistentVolumeClaim named `redisdb-pvc` with a request for `1Gi` of storage. Make sure it has the same access mode as the PersistentVolume

* Create a pod named `redispod` using the `redis image` and a container name of `redisdb`. The mount path on the container must be `/data` and you must open port `6379` on the container. Make sure you mount the same PVC that you created in the last step.

* Connect to the container by running the `redis-cli` command from within the container. Use the `SET` command to apply the key space `server:name` as `"redis server"`. Use the `GET` command to verify that the `server:name` keyspace has been set. Use the `QUIT` command to exit the redis-cli

* Delete the pod named redispod

* Change the name of the pod to `redispod2`. Create the new pod with that YAML spec.

* Connect to the `redispod2` container and run the `redis-cli` from within the container. Run the command `GET server:name` to retrieve the keyspace that we set with the previous pod. The result will be `"redis server"`, which means the data persisted from redispod to redispod2.

![](./img/CKA-LABS_%20Creating%20persistent%20volumes%20for%20pods%20in%20Kubernetes.png)