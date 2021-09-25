# k8s-cka-final
Chuẩn bị môi trường GCP
```
$ gcloud config list
![image](https://user-images.githubusercontent.com/54676613/134762683-bfa2ed9f-3042-4dc7-b0c4-cb3d363c2f9d.png)

$ gcloud compute firewall-rules create nodeports --allow tcp:30000-40000
$ gcloud compute firewall-rules create kube-api-server --allow tcp:6443

$ gcloud compute instances create kube-master \
--machine-type=e2-medium \
--image=ubuntu-1804-bionic-v20210817 \
--image-project=ubuntu-os-cloud \
--boot-disk-size=200GB

$ for i in 1 2; do
gcloud compute instances create kube-worker${i} \
    --machine-type=e2-medium \
    --image=ubuntu-1804-bionic-v20210817 \
    --image-project=ubuntu-os-cloud \
    --boot-disk-size=200GB
done
```
Kiểm tra các VM đã tạo trên GCP
```
$ gcloud compute instances list
![image](https://user-images.githubusercontent.com/54676613/134762775-c1ac9b85-cf0e-487d-8eb9-72f792ccb185.png)
```
