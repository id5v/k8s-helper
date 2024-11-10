

sudo -i 

git clone git@gitlab.slurm.io:edu/k8s_mega/practice.git

[kubespray]
https://habr.com/ru/companies/domclick/articles/682364/

[terraform]
terragrand

cat /etc/os-release

[Обновление всех зависемостей]
dnf update -y

[run]
yum-config-manager \
--add-repo \
https://download.docker.com/linux/centos/docker-ce.repo
[resp]
Adding repo from: https://download.docker.com/linux/centos/docker-ce.repo

[run]
dnf install -y containerd.io-1.7.22-3.1.e19
mkdir -p /etc/containerd

systemctl restart containerd

systemctl status containerd.service

# Step 1: Download and extract crictl
curl -L https://github.com/kubernetes-sigs/cri-tools/releases/download/v1.31.1/crictl-v1.31.1-linux-amd64.tar.gz | tar -zxf - -C /usr/bin

# Step 2: Configure crictl
cat <<EOF > /etc/crictl.yaml
runtime-endpoint: unix:///var/run/containerd/containerd.sock
image-endpoint: unix:///var/run/containerd/containerd.sock
timeout: 30
debug: false
EOF

curl -L https://github.com/containerd/nerdctl/releases/download/v1.7.7/nerdctl-1.7.7-linux-amd64.tar.gz | tar -zxf - -C /usr/bin

crictl ps

nerdctl --help

cat <<EOF > /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

sysctl --system

sestatus

Если вклюбчен Может блокировать компоненты так как включен по дефолту
для выключения сделать

setenforce 0
sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

для синхронизации воемени на нодах
systemctl enable --now ntpd

ntpq -p


dnf install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

systemctl enable --now kubelet

systemctl status kubelet

ip a или cat /etc/hosts

172.17.79.2/24
172.17.79.5
172.17.79.5 ingress-1.s073036 ingress-1.s073036.slurm.io

kubeadm reset

kubeadm init --config cluster.yaml --upload-certs | tee -a kubeadm_init.log

сохранятся все join  комады kubeadm_init.log для присоединения оставшихся мастеров 2 и 3 и воркер нод  1 и 2

kubeadm join 172.17.79.5:6443 --token 4ikx21.1gonzzrt7lhjhbnh \
    --discovery-token-ca-cert-hash sha256:9a186738232438760ecd631675b397a70a23feee4b81528704fb6daeb13ab432 \
    --control-plane --certificate-key 86a52a6816d0f440ba442fd40c03f3a2f4b25a8361a1d54b82b7a5887d6f0f56

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

Посмотреть ноды 
kubectl get nodes

kubectl get pods -A

kubectl -n kube-system describe po coredns-55cb58b774-bn22v

kubectl apply -f calico_3.28.2.yaml

kubectl apply -f calico_3.28.2.yaml --validate=false
 


haproxy cat /etc/haproxy/haproxy.cfg - настройки балансировщика







Илья Данилов
Логин: s073036
Пароль: 17e9521c