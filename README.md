# k8s-cka-final
Chuẩn bị môi trường GCP
```
$ gcloud config list
![image](https://user-images.githubusercontent.com/54676613/134762880-7b07d414-aa5d-4841-a907-0905562cf6d1.png)


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
![image](https://user-images.githubusercontent.com/54676613/134762887-396be916-9903-4557-a603-b262ae009bd0.png)
```
