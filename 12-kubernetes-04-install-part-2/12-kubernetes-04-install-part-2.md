# Решение домашнего задания к занятию "12.4 Развертывание кластера на собственных серверах, лекция 2"

## Задание 1: Подготовить инвентарь kubespray

[hosts.ini](./hosts.ini)
```
all:
  hosts:
    srv-cl-master-1:
      ansible_host: 10.100.104.63
      ansible_user: a.chernyh
    srv-cl-worker-1:
      ansible_host: 10.100.104.64
      ansible_user: a.chernyh
    srv-cl-worker-2:
      ansible_host: 10.100.104.65
      ansible_user: a.chernyh
    srv-cl-worker-3:
      ansible_host: 10.100.104.66
      ansible_user: a.chernyh
    srv-cl-worker-4:
      ansible_host: 10.100.104.67
      ansible_user: a.chernyh
  children:
    kube_control_plane:
      hosts:
        srv-cl-master-1:
    kube_node:
      hosts:
        srv-cl-worker-1:
        srv-cl-worker-2:
        srv-cl-worker-3:
        srv-cl-worker-4:
    etcd:
      hosts:
        srv-cl-master-1:
    k8s_cluster:
      children:
        kube_control_plane:
        kube_node:
    calico_rr:
      hosts: {}

```