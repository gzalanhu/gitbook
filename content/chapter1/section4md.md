# 第一章 / 第四節
安装完成之后就是启动脚本了

master上的启动脚本为kubernetesstart.sh  
    #!/bin/bash
    
    etcd --listen-peer-urls http://0.0.0.0:2380 --data-dir=/var/lib/etcd --listen-client-urls http://0.0.0.0:2379 --advertise-client-urls     http://master:2379 >> /var/log/etcd 2>&1 &
    sleep 2
    etcdctl set /coreos.com/network/config '{ "Network": "10.1.0.0/16" }'
    flanneld --listen=0.0.0.0:8888 >> /var/log/flanneld 2>&1 &
    docker -d -H unix:///var/run/docker.sock -H tcp://0.0.0.0:2375 >> /var/log/dockerd 2>&1 &
    kube-apiserver --logtostderr=true --v=0 --etcd_servers=http://master:2379 --address=0.0.0.0 --allow_privileged=false --service-cluster-ip    -range=10.254.0.0/16 --v=0 >> /var/log/kubernetes/kube-apiserver 2>&1 &
    kube-controller-manager --logtostderr=true --v=0 --master=http://master:8080 --v=0 --node-monitor-grace-period=10s --pod-eviction-    timeout=10s >> /var/log/kubernetes/kube-controller-manager 2>&1 &
    kube-scheduler --logtostderr=true --v=0 --master=http://master:8080 >> /var/log/kubernetes/kube-scheduler 2>&1 &



node上的启动脚本为nodestart.sh  
    #!/bin/bash
    
    flanneld -etcd-endpoints=http://master:2379 -remote=master:8888 >> /var/log/flannel 2>&1 &
    sleep 2
    source /run/flannel/subnet.env
    docker -d -H unix:///var/run/docker.sock -H tcp://0.0.0.0:2375 >> /var/log/dockerd --bip=${FLANNEL_SUBNET} --mtu=${FLANNEL_MTU} 2>&1 &
    kubelet --logtostderr=true --v=0 --api_servers=http://master:8080 --address=0.0.0.0 --allow_privileged=false > /var/log/kubernetes/    kubelet 2>&1 &
    kube-proxy --logtostderr=true --v=0 --master=http://master:8080 > /var/log/kubernetes/kube-proxy 2>&1 &
