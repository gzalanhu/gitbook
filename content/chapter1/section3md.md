# 第一章 / 第三節

此所有操作都在192.168.20.207(node上执行,其他node一样)
其实node安装方法更简单,就把master上的几个文件拷贝过来好了  

安装Docker  

curl -sSL https://get.daocloud.io/docker | sh

node上用的文件有kube-proxy,kubelet,flanneld,etcd  
cd /usr/local/bin/  
wget http://download.123cw.cn/centos/kubernetes/kube-proxy  
wget http://download.123cw.cn/centos/kubernetes/kubelet  
wget http://download.123cw.cn/centos/kubernetes/flanneld  
wget http://download.123cw.cn/centos/kubernetes/etcd  

搞定收工! 
