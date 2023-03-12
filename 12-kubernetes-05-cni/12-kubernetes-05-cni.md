# Решение домашнего задания к занятию "12.5 Сетевые решения CNI"

## Задание 1: установить в кластер CNI плагин Calico
```
a.chernyh@srv-cl-master-1:~$ create deployment hello-world --namespace default --image=nginx:latest
deployment.apps/hello-world created
a.chernyh@srv-cl-master-1:~$ kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
hello-world-654975c8cd-4gqv6   1/1     Running   0          16s
a.chernyh@srv-cl-master-1:~$ kubectl get deployment
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
hello-world   1/1     1            1           89s
```
```
a.chernyh@srv-cl-master-1:~$ kubectl apply -f network-policy/policy-allow.yaml
networkpolicy.networking.k8s.io/policy-allow created
a.chernyh@srv-cl-master-1:~$ kubectl get networkpolicies
NAME           POD-SELECTOR      AGE
policy-allow   app=hello-world   2m49s
```
## Задание 2: изучить, что запущено по умолчанию
```
a.chernyh@srv-cl-master-1:~$ ./calicoctl get nodes --allow-version-mismatch
NAME
srv-cl-master-1
srv-cl-worker-1
srv-cl-worker-2
srv-cl-worker-3
srv-cl-worker-4
node4
a.chernyh@srv-cl-master-1:~$ ./calicoctl get ipPool --allow-version-mismatch
NAME           CIDR             SELECTOR
default-pool   10.233.64.0/18   all()
a.chernyh@srv-cl-master-1:~$ ./calicoctl get profile --allow-version-mismatch
NAME
projectcalico-default-allow
kns.default
kns.kube-node-lease
kns.kube-public
kns.kube-system
ksa.default.default
ksa.kube-node-lease.default
ksa.kube-public.default
ksa.kube-system.attachdetach-controller
ksa.kube-system.bootstrap-signer
ksa.kube-system.calico-node
ksa.kube-system.certificate-controller
ksa.kube-system.clusterrole-aggregation-controller
ksa.kube-system.coredns
ksa.kube-system.cronjob-controller
ksa.kube-system.daemon-set-controller
ksa.kube-system.default
ksa.kube-system.deployment-controller
ksa.kube-system.disruption-controller
ksa.kube-system.dns-autoscaler
ksa.kube-system.endpoint-controller
ksa.kube-system.endpointslice-controller
ksa.kube-system.endpointslicemirroring-controller
ksa.kube-system.ephemeral-volume-controller
ksa.kube-system.expand-controller
ksa.kube-system.generic-garbage-collector
ksa.kube-system.horizontal-pod-autoscaler
ksa.kube-system.job-controller
ksa.kube-system.kube-proxy
ksa.kube-system.namespace-controller
ksa.kube-system.node-controller
ksa.kube-system.nodelocaldns
ksa.kube-system.persistent-volume-binder
ksa.kube-system.pod-garbage-collector
ksa.kube-system.pv-protection-controller
ksa.kube-system.pvc-protection-controller
ksa.kube-system.replicaset-controller
ksa.kube-system.replication-controller
ksa.kube-system.resourcequota-controller
ksa.kube-system.root-ca-cert-publisher
ksa.kube-system.service-account-controller
ksa.kube-system.service-controller
ksa.kube-system.statefulset-controller
ksa.kube-system.token-cleaner
ksa.kube-system.ttl-after-finished-controller
ksa.kube-system.ttl-controller
vagrant@vagrant:~/netology-12-kubernetes-05-cni$
```
