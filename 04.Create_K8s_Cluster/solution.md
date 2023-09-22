## Install Docker and Kubernetes on All Servers

### Note: Step 1-9 on all 3 servers

1. SSH into the servers and elevate sudo privileges
`sudo su`

2. Disable SELinux
```
setenforce 0
sed -i --follow-symlinks 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux
```

3. Enable the br_netfilter module for cluster communication
```
modprobe br_netfilter
echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables
```

4. Install Docker dependencies
```
yum install -y yum-utils device-mapper-persistent-data lvm2
```

5. Add the Docker repo and install Docker
```
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install -y docker-ce
```

6. Set the cgroup driver for Docker to systemd, reload systemd, then enable and start Docker
```
sed -i '/^ExecStart/ s/$/ --exec-opt native.cgroupdriver=systemd/' /usr/lib/systemd/system/docker.service
systemctl daemon-reload
systemctl enable docker --now
```

7. Add the Kubernetes repo
```
cat << EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
  https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```

8. Install Kubernetes v1.14.0
```
yum install -y kubelet-1.14.0-0 kubeadm-1.14.0-0 kubectl-1.14.0-0 kubernetes-cni-0.7.5
```

9. Enable the kubelet service.
```
systemctl enable kubelet
```

* Note: The kubelet service will fail to start until the cluster is initialized.

### Note: Complete the following section on the MASTER ONLY!

10. Initialize the cluster using the IP range for Flannel:
```
kubeadm init --pod-network-cidr=10.244.0.0/16
```

11. Copy the `kubeadmn join ...` command that is in the output.

12. Exit `sudo`, copy the `admin.conf` to your home directory, and take ownership.
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

13. Deploy Flannel
```
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel-old.yaml
```

14. Check the cluster state
```
kubectl get pods --all-namespaces
```

* Note: The flannel pods must be running

### Note: Complete the following steps on the NODES ONLY!

15. Run the `kubeadm join ...` command that you copied earlier, this requires running the command prefaced with `sudo` on the nodes. 

16. Then we'll check the nodes from the master node
```
kubectl get nodes
```

## Create and Scale a Deployment Using kubectl

### Note: These commands will only be run on the master node.

17. Create a simple deployment
```
kubectl create deployment nginx --image=nginx
```

18. Inspect the pod
```
kubectl get pods
```

19. Scale the deployment
```
kubectl scale deployment nginx --replicas=4
```

20. Inspect the pods. There should be four pods now
```
kubectl get pods
```
