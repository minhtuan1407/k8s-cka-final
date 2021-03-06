# 1. Tạo 1 kubernetes cluster bao gồm 1 master + 2 workers. Liệt kê các node của cluster và thông tin chi tiết: ROLES, INTERNAL-IP, EXTERNAL-IP, ...
## Command trên cả 3 node
```
$ sudo apt-get update
$ sudo apt-get install -y apt-transport-https ca-certificates curl
$ curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
$ echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

$ KUBE_VERSION=1.21.0
$ sudo apt-get install -y \
  docker.io \
  kubelet=${KUBE_VERSION}-00 \
  kubeadm=${KUBE_VERSION}-00 \
  kubectl=${KUBE_VERSION}-00
$ sudo apt-mark hold kubelet kubeadm kubectl

$ sudo bash -c 'cat > /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "storage-driver": "overlay2"
}
EOF'

$ sudo mkdir -p /etc/systemd/system/docker.service.d

$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
$ sudo systemctl enable docker

$ sudo docker info | grep -i "storage"
$ sudo docker info | grep -i "cgroup"

$ sudo systemctl enable kubelet
$ sudo systemctl start kubelet
```
## Command chỉ nhập trên node kube-master
```
# Khi chạy command này sẽ ra được dòng output cuối cùng để nhập trên 2 node worker
$ sudo kubeadm init --apiserver-cert-extra-sans=35.198.208.19 --kubernetes-version=${KUBE_VERSION}

$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
## Command chỉ nhập kube-worker1 và kube-worker2
```
# Lấy dòng output cuối cùng của command "sudo kubeadm init" để join 2 node worker vào cluster
$ sudo kubeadm join 10.148.0.5:6443 \
      --token u2vno2.fxunfaa7pmp1h5vq \   
      --discovery-token-ca-cert-hash sha256:3fb1705a4afb0a8e5b5af93f0105e18b6df33e87b444f1a7be516d0e8b6e783a
```
## Command chỉ nhập trên node kube-master để cài CNI cho cluster
```
$ kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
```
## Command chỉ nhập trên node kube-master để kiểm tra cluster 
```
$ kubectl get nodes -owide
```
![image](https://user-images.githubusercontent.com/54676613/134764135-c71883af-5f49-4d8f-b134-de987893ff45.png)

# 2. Tạo 1 deployment tên là webapp với 2 replica, sử dụng image nginx 1.18.0. Kiểm tra trạng thái của deployment và pod.
```
$ kubectl create deployment webapp --image=nginx:1.18.0

$ kubectl scale deployment webapp --replicas=2

$ kubectl get pod -l app=webapp -owide

$ kubectl get deployment -l app=webapp -owide
```
![image](https://user-images.githubusercontent.com/54676613/134764294-6a2a6ceb-a415-4422-95fb-fa73d88a7f0d.png)

# 3. Expose webapp sử dụng một dịch vụ dạng NodePort.
```
$ kubectl expose deployment webapp --type NodePort --port 80
```
![image](https://user-images.githubusercontent.com/54676613/134764337-9cb385a8-4b60-4c23-ada6-62c27a549479.png)

# 4. Chạy lệnh curl để truy cập vào webapp.
```
# Đứng ở pod trong cluster curl
$ kubectl run bb -it --rm --image radial/busyboxplus:curl --restart Never -- curl http://webapp
```
![image](https://user-images.githubusercontent.com/54676613/134764324-9a30709d-8226-4e25-9612-6fed21c1a277.png)

```
# Đứng ở 1 node bất kỳ curl
$ curl http://10.99.20.187
```
![image](https://user-images.githubusercontent.com/54676613/134764347-20ee5ed6-a168-439d-bfe5-248442741e37.png)

```
# Đứng ở public curl 3 IP public của 3 node GCP
$ curl http://35.198.208.19:32651
$ curl http://35.198.219.50:32651
$ curl http://35.186.145.245:32651
```
![image](https://user-images.githubusercontent.com/54676613/134764440-47b77397-c9b3-4ff0-af88-5ec03d428947.png)
