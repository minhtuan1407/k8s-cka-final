# Tạo một deployment tên là webapp2, với 1 label là “app:web2" với 2 replica, sử dụngimage là nginx:latest và expose ra port 80 trên một ClusterIP service.

# Tạo một Network Policy với tên là access-web cho phép chỉ những pod với label "access:accepted" có thể truy cập deployment này. Triển khai Network Policy này.

# Tạo một pod với tên là busybox thoả mãn điều kiện của Network Policy để kiểm tra vào webapp2 deployment thông qua ClusterIP service. Chạy lệnh wget trên pod này để truy cập vào webapp.
