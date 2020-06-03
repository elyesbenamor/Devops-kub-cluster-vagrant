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
