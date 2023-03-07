# Решение домашнего задания к занятию "12.1 Компоненты Kubernetes"

## Задача 1: Установить Minikube

```
PS C:\Windows\system32> minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

PS C:\Windows\system32> kubectl get pods --namespace=kube-system
NAME                               READY   STATUS    RESTARTS      AGE
coredns-787d4945fb-7dkm9           1/1     Running   0             67s
etcd-minikube                      1/1     Running   0             80s
kube-apiserver-minikube            1/1     Running   0             82s
kube-controller-manager-minikube   1/1     Running   0             82s
kube-proxy-69rkr                   1/1     Running   0             67s
kube-scheduler-minikube            1/1     Running   0             80s
storage-provisioner                1/1     Running   1 (51s ago)   78s
```


## Задача 2: Запуск Hello World

```
PS C:\Windows\system32> kubectl get pod,svc -n kube-system
NAME                                   READY   STATUS    RESTARTS      AGE
pod/coredns-787d4945fb-7dkm9           1/1     Running   0             10m
pod/etcd-minikube                      1/1     Running   0             10m
pod/kube-apiserver-minikube            1/1     Running   0             10m
pod/kube-controller-manager-minikube   1/1     Running   0             10m
pod/kube-proxy-69rkr                   1/1     Running   0             10m
pod/kube-scheduler-minikube            1/1     Running   0             10m
pod/metrics-server-5f8fcc9bb7-bgn92    1/1     Running   0             6m51s
pod/storage-provisioner                1/1     Running   1 (10m ago)   10m

NAME                     TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)                  AGE
service/kube-dns         ClusterIP   10.96.0.10     <none>        53/UDP,53/TCP,9153/TCP   10m
service/metrics-server   ClusterIP   10.98.24.138   <none>        443/TCP                  6m51s
```
```
PS C:\Windows\system32> minikube addons list
|-----------------------------|----------|--------------|--------------------------------|
|         ADDON NAME          | PROFILE  |    STATUS    |           MAINTAINER           |
|-----------------------------|----------|--------------|--------------------------------|
| ambassador                  | minikube | disabled     | 3rd party (Ambassador)         |
| auto-pause                  | minikube | disabled     | Google                         |
| cloud-spanner               | minikube | disabled     | Google                         |
| csi-hostpath-driver         | minikube | disabled     | Kubernetes                     |
| dashboard                   | minikube | enabled ✅   | Kubernetes                     |
| default-storageclass        | minikube | enabled ✅   | Kubernetes                     |
| efk                         | minikube | disabled     | 3rd party (Elastic)            |
| freshpod                    | minikube | disabled     | Google                         |
| gcp-auth                    | minikube | disabled     | Google                         |
| gvisor                      | minikube | disabled     | Google                         |
| headlamp                    | minikube | disabled     | 3rd party (kinvolk.io)         |
| helm-tiller                 | minikube | disabled     | 3rd party (Helm)               |
| inaccel                     | minikube | disabled     | 3rd party (InAccel             |
|                             |          |              | [info@inaccel.com])            |
| ingress                     | minikube | enabled ✅   | Kubernetes                     |
| ingress-dns                 | minikube | disabled     | Google                         |
| istio                       | minikube | disabled     | 3rd party (Istio)              |
| istio-provisioner           | minikube | disabled     | 3rd party (Istio)              |
| kong                        | minikube | disabled     | 3rd party (Kong HQ)            |
| kubevirt                    | minikube | disabled     | 3rd party (KubeVirt)           |
| logviewer                   | minikube | disabled     | 3rd party (unknown)            |
| metallb                     | minikube | disabled     | 3rd party (MetalLB)            |
| metrics-server              | minikube | enabled ✅   | Kubernetes                     |
| nvidia-driver-installer     | minikube | disabled     | Google                         |
| nvidia-gpu-device-plugin    | minikube | disabled     | 3rd party (Nvidia)             |
| olm                         | minikube | disabled     | 3rd party (Operator Framework) |
| pod-security-policy         | minikube | disabled     | 3rd party (unknown)            |
| portainer                   | minikube | disabled     | 3rd party (Portainer.io)       |
| registry                    | minikube | disabled     | Google                         |
| registry-aliases            | minikube | disabled     | 3rd party (unknown)            |
| registry-creds              | minikube | disabled     | 3rd party (UPMC Enterprises)   |
| storage-provisioner         | minikube | enabled ✅   | Google                         |
| storage-provisioner-gluster | minikube | disabled     | 3rd party (Gluster)            |
| volumesnapshots             | minikube | disabled     | Kubernetes                     |
|-----------------------------|----------|--------------|--------------------------------|
```
![image](https://user-images.githubusercontent.com/42215603/223510453-9300a2e3-a815-416b-abbb-ddb02e66141e.png)


## Задача 3: Установить kubectl

```
PS C:\Windows\system32> kubectl port-forward service/hello-node 8090:8080
Forwarding from 127.0.0.1:8090 -> 8080
Forwarding from [::1]:8090 -> 8080
Handling connection for 8090
Handling connection for 8090
```
