How to install  kubernets cluster on Ubuntu 20.04 using Kubeadm method without any errors within 5minites on AWS EC2 instance 


Prerequisites :
2 or 3 Ubuntu 20.04 LTS System with Minimal Installation
Minimum 2 or more CPU, 4 GB RAM. Master  node
Minimum 1 or more CPU, 2 GB RAM, for Worker Node


Step1: Install Docker engine and kubeadm  Runtime on All node (Master and Worker Nodes)

To run below commands On Master & worker node by using Nano edit tab run as root user 
Refer attached images 

apt-get update  
apt-get install docker.io -y
service docker restart  
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -  
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >/etc/apt/sources.list.d/kubernetes.list
apt-get update
apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y  

 
sudo su     ( use this command for both Master and worker Node for root user) 
use nano install.sh command for install docker and K8s bellow commands save and
to run the command   sh install.sh  

Step2: Join Worker Node to the Cluster
On Master:
1.	kubeadm init --pod-network-cidr=192.168.0.0/16
   >Copy the token and paste it into the worker node.
 
Step3:  To be able to run kubectl commands as non-root user
On Master:
  Exit and bellow 3 commands in master node 
1.	mkdir -p $HOME/.kube
2.	sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
3.	sudo chown $(id -u):$(id -g) $HOME/.kube/config


  
step4: Deploy Calico network
On Master:
1  curl https://raw.githubusercontent.com/projectcalico/calico/v3.25.0/manifests/calico.yaml -O
2   kubectl apply -f calico.yaml
3 kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml


Our Kubernetes installation and configuration are complete

Step5: Verifying the cluster 
On Master:
1 kubectl get nodes


 

