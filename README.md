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
### 3- Setup Host file on each server
```
sudo vi /etc/hosts
```
##### Add private ip address of each server ( only the last three to other servers)

```
127.0.0.1 localhost
# The following lines are desirable for IPv6 capable hosts
::1 ip6-localhost ip6-loopback
172.31.100.74   83e98b9a251c.mylabserver.com
172.31.100.74 k8s-master
172.31.106.83 k8s-worker1
172.31.111.55 k8s-worker2
```
###### Save and exit on each server , Then logout of each server and login again

### 4- Install COntainerd on each server
```
cat << EOF | sudo tee /etc/modules-load.d/containerd.conf
```
```
> overlay
> br_netfilter
> EOF
[sudo] password for cloud_user:
overlay
br_netfilter
```
###### Enable these modules
```
sudo modprobe overlay
```
```
sudo modprobe br_netfilter
```
##### Add configuration that k8s will need
```
cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf
```
```
> net.bridge.bridge-nf-call-iptables = 1
> net.ipv4.ip_forward = 1
> net.bridge.bridge-nf-call-ip6tables = 1
> EOF
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-ip6tables = 1
```
####### Apply them Immediately
```
sudo sysctl --system
```
##### Install Containerd
```
sudo apt-get update && sudo apt-get install -y containerd
```
##### Steup Conatainerd Configuration file
```
sudo mkdir -p /etc/containerd
```
```
sudo containerd config default | sudo tee /etc/containerd/config.toml
```
######## To make sure that containerd is using that configuration , we will restart it
```
sudo systemctl restart containerd
```
### 5- Install K8s packages
##### Disable swapoff
```
sudo swapoff -a
```
##### Install packages
```
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
```

