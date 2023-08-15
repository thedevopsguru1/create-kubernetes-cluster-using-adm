# create-kubernetes-cluster-using-adm
#### Go to cloud guru , then plyaground , finall cloud server
### 2- Setup Hostname
```
sudo hostnamectl set-hostname k8s-master
```
```
sudo hostnamectl set-hostname k8s-workerx
```
###### Check it 
```
hostname
```
### 3- Setup Host file on master
```
sudo vi /etc/hosts
```
##### Add private ip address of each server

```
127.0.0.1 localhost
# The following lines are desirable for IPv6 capable hosts
::1 ip6-localhost ip6-loopback
172.31.100.74   83e98b9a251c.mylabserver.com
172.31.100.74 k8s-master
172.31.106.83 k8s-worker1
172.31.111.55 k8s-worker2
```
