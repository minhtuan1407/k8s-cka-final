# 1. Tạo một pod đặt tên là web, sử dụng image nginx:latest thoả mãn điều kiện chỉ chạy master node, không được schedule lên worker node.
```
# Cho phép control plan chạy workload trên đó
$ kubectl taint nodes kube-master node-role.kubernetes.io/master-

# Tạo label cho master node ví dụ như disktype
$ kubectl label nodes kube-master disktype=ssd

$ kubectl apply -f https://raw.githubusercontent.com/minhtuan1407/k8s-cka-final/main/cau4/pod.yaml
```
# 2. Kiểm tra trạng thái để chắc chắn pod được khởi tạo và vận hành bình thường trên master node
```
$ kubectl get pod -l app=web
```
