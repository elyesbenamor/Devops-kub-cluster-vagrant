# Devops-kub-cluster-vagrant
Creating a Kubernetes cluster on a virtual machine using Vagrant 
****************************************************************

1st Step: create a ubuntu vm using vagrant
--
use vagrant directory and type :
-----------------------------------------------------
$ sudo vagrant up 

a ubuntu vm will come up then ssh to it using :

$ vagrant ssh
2nd Step: Clone the repo into your new vm 
--

we have multiple files in vagrant-provisionning , i will explain them one by one.

Vagrantfile
--
this file is gonna lunch 1 master and 2 workers based on centos7 machine .

the master node and worker nodes will require bootsrap.sh file .

Master node named "kmaster" will require also "bootstrap_kmaster.sh"
Worker nodes : kworker1 kworker2 will require "bootstrap_kworker.sh"

bootstrap.sh
--
Using NFS-Client provisioner 
--------------------------------------------------------
In order to use dynamic provisioning we will mout a directory from our hardware and bind it with the nfs-client pod so we can use it as provisionner to dunamically bind PV to our apps.


For that we will first copy the admin conf file to our hardware:


1/scp root@"your ip address for the kmaster":/etc/kubernetes/admin.conf ~/.kube/conf

then you can access your cluster from your laptop without ssh to your nodes


2/ create a directory called /srv/nfs/kubedata in local machine 

chown nobody:/srv/nfs/kubedata

nano /etc/exports

/srv/nfs/kubedata     *(rw,sync,no_subtree_check,no_root_squash,no_all_squash,insecure)

"tah * mean expose it for everyone"

systemctl restart nfs-server

3/ on the other server install nfs client then create a directory , i am going to call it mnt

mkdir mnt

mount -t nfs x:/home /mnt/nfs/home/  where x = your ip address of your local machine 

Deploying NFS provisioner
---------------------------------------------
to install nfs provisioner : 

kubectl create -f ./nfs

Desploying Jenkins Server
---------------------------------------------------
