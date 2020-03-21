# Install Oracle VM VirtualBox version 6.1.4 on my laptop
Follow this documentation to install Oracle VM VirtualBox version 6.1.4

This documentation guides you in setting up a cluster with one master node and one worker node.

## Verify what version of Linux OS i have on my laptop
☁  docs [master] ⚡  cat /etc/lsb-release  
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=19.10
DISTRIB_CODENAME=eoan
DISTRIB_DESCRIPTION="Ubuntu 19.10"
☁  docs [master] ⚡  
```
## Go the web site of Oracle VM VirtualBox to download the package
https://www.virtualbox.org
- Cliquer sur Downloads
- Cliquer sur Linux Distributions
- Cliquer sur Ubuntu 19.10
```
  
|Role|FQDN|IP|OS|RAM|CPU|
|----|----|----|----|----|----|
|Master|kmaster.example.com|172.42.42.100|CentOS 7|2G|2|
|Worker|kworker.example.com|172.42.42.101|CentOS 7|1G|1|

## On both Kmaster and Kworker
Perform all the commands as root user unless otherwise specified
### Pre-requisites
##### Update /etc/hosts
So that we can talk to each of the nodes in the cluster
```
cat >>/etc/hosts<<EOF
172.42.42.100 kmaster.example.com kmaster
172.42.42.101 kworker.example.com kworker
EOF
```
##### Install, enable and start docker service
Use the Docker repository to install docker.
> If you use docker from CentOS OS repository, the docker version might be old to work with Kubernetes v1.13.0 and above
```
yum install -y -q yum-utils device-mapper-persistent-data lvm2 > /dev/null 2>&1
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo > /dev/null 2>&1
yum install -y -q docker-ce >/dev/null 2>&1

systemctl enable docker
systemctl start docker
```

