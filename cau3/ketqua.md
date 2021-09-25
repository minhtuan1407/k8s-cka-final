# 1. Tạo một deployment tên là webapp2, với 1 label là “app:web2" với 2 replica, sử dụng image là nginx:latest và expose ra port 80 trên một ClusterIP service.
```
$ kubectl apply -f https://raw.githubusercontent.com/minhtuan1407/k8s-cka-final/main/cau3/webapp2.yaml
```
# 2. Tạo một Network Policy với tên là access-web cho phép chỉ những pod với label "access:accepted" có thể truy cập deployment này. Triển khai Network Policy này.
```
$ kubectl apply -f https://raw.githubusercontent.com/minhtuan1407/k8s-cka-final/main/cau3/access-web.yaml
```
# 3. Tạo một pod với tên là busybox thoả mãn điều kiện của Network Policy để kiểm tra vào webapp2 deployment thông qua ClusterIP service. Chạy lệnh wget trên pod này để truy cập vào webapp.
```
$ kubectl run test-$RANDOM --rm -i -t --image=alpine --labels access=accepted -- sh
/ # wget -qO- --timeout=2 http://webapp2

$ kubectl run test-$RANDOM --rm -i -t --image=alpine -- sh
/ # wget -qO- --timeout=2 http://webapp2
```
wget: download timed out
