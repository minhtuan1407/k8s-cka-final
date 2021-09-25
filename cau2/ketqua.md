# 1. Tạo một namespace với tên cau2.
```
$ kubectl create namespace cau2
```

# 2. Tạo một pod vớt tên pod2 với 2 container lần lượt với tên c1 và c2, một volume tên vol gắn với pod và được mount tới mọi container trong đó nhưng không cố định và không chia sẻ với các pod khác.

# 3. Container c1 sử dụng image busybox:1.31.1 và ghi kết quả của lệnh date vào file /vol/date.log mỗi 5 giây trên shared volume.

# 4. Container c2 sử dụng image busybox:1.31.1 liên tục xuất nội dung của date.log ra màn hình sử dụng lệnh tail.

# 5. Kiểm tra log của container c2 và ghi kết quả
