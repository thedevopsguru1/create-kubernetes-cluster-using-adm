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

