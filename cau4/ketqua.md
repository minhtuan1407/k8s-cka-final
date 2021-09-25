# 1. Tạo một pod đặt tên là web, sử dụng image nginx:latest thoả mãn điều kiện chỉ chạy master node, không được schedule lên worker node.
```
# Tạo label cho master node ví dụ như disktype
$ kubectl label nodes kube-master disktype=ssd

$ 
```
# 2. Kiểm tra trạng thái để chắc chắn pod được khởi tạo và vận hành bình thường trên master node
```
$ kubectl get pod
```
