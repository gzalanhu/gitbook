# 第一章 / 第一節

Kubernetes是google开源的一个容器集群管理软件.据说好牛逼具体我就不说了,百度吧
现在我们说说我们的环境,Kubernetes是CS架构的,网上有好多安装方法,比较好用跟容易的就是用CentOS7咯,yum一下就可以了.但是不是所有人都是用Centos的.而且据说Centos对Docker的兼容性不好.所以我这里说的通用的办法吧.说说我的环境:  

192.168.20.138:Master  

   环境:  

      -Docker  

      -Kubernetes(kube-apiserver,kube-controller-manager,kube-scheduler)  

      -flanneld  

      -etcd   


192.168.20.207:Node  

   环境:  

      -Docker  

      -Kubernetes(kube-proxy,kubelet)  

      -flanneld  


两台机器安装的都是 ubuntu14.04  


所有包的下载地址我已经放我们自己服务器了  


```wget http://download.123cw.cn/centos/kubernetes/etcd-v2.1.2-linux-amd64.tar.gz  

wget http://download.123cw.cn/centos/kubernetes/kubernetes.tar.gz   ```

