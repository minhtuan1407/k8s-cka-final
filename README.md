# k8s-cka-final
Chuẩn bị môi trường GCP
```
$ gcloud config list
[compute]
region = asia-southeast1
zone = asia-southeast1-c
[core]
account = m.tuan9a2@gmail.com
disable_usage_reporting = False
project = learn-kubernetes-326814


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
NAME          ZONE               MACHINE_TYPE  PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP     STATUS
kube-master   asia-southeast1-c  e2-medium                  10.148.0.5   35.198.208.19   RUNNING
kube-worker1  asia-southeast1-c  e2-medium                  10.148.0.6   35.198.219.50   RUNNING
kube-worker2  asia-southeast1-c  e2-medium                  10.148.0.7   35.186.145.245  RUNNING
```
