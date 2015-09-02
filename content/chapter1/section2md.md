# 第一章 / 第二節

此所有操作都在192.168.20.138(Master上执行)  
cd /data/softsrc   

wget http://download.123cw.cn/centos/kubernetes/etcd-v2.1.2-linux-amd64.tar.gz  


wget http://download.123cw.cn/centos/kubernetes/kubernetes.tar.gz  

安装etcd:  
tar zxvf etcd-v2.1.2-linux-amd64.tar.gz  
cd etcd-v2.1.2-linux-amd64  
cp etcd* /usr/local/bin/  

安装kubernetes:  
cd /data/softsrc  
tar zxvf kubernetes.tar.gz  
cd /data/softsrc/kubernetes/server/  
tar zxvf kubernetes-server-linux-amd64.tar.gz  
cp kubernetes/server/bin/kube* /usr/local/bin  

生成二进制文件:  
cd /data/softsrc/kubernetes/cluster/ubuntu(因为是ubuntu系统)  
./build.sh  
然后下载一批编译好的二进制文件  
cp -rf  binaries/master/flanneld  /usr/local/bin  

安装Docker  
curl -sSL https://get.daocloud.io/docker | sh  

至此,kubernetes集群的Master安装完成!

 
