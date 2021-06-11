# k8s-install

# 1.kubernetes.repo

添加k8s的源，将该文件放到/etc/yum.repos.d/目录下

yum clean

yum update

yum install -y kubectl-1.19.2 kubeadm-1.19.2 kubelet-1.19.2 

# 2.image.sh

执行文件下载镜像

sh image.sh
也可不使用这个，因为在第三步中已经配置好了要使用的镜像，镜像不改名也可以的

# 3.kubeadm-master.config

初始化第一个master节点，这里需要修改里面的ip地址为本服务器的ip

kubeadm init --config=kubeadm-master.config

复制配置文件使得可以通过命令行查看k8s状态，如kubectl get nodes

  mkdir -p $HOME/.kube
  
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

# 4.kube-flannel.yml

安装网络插件，使master节点由notready转为ready

kubectl apply -f kube-flannel.yml

# 5.scp.sh

复制配置文件到其他master节点，这里需要修改ip地址，如果为多个master中间用空格分开即可

sh scp.sh
