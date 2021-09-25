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
$ kubectl get pod -owide -l app=web
```
![image](https://user-images.githubusercontent.com/54676613/134765158-1114c77e-edfd-4994-bfc1-4cb9dcc2c9b2.png)
```
$ curl http://10.32.0.2
```
![image](https://user-images.githubusercontent.com/54676613/134765172-8565a227-8f14-436c-8f60-dbc1ab0870cd.png)
