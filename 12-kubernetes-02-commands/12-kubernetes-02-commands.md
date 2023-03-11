# Решение домашнего задания к занятию "12.2 Команды для работы с Kubernetes"

## Задание 1: Запуск пода из образа в деплойменте
Создал Deployment с nginx, чтобы в дальнейшем посмотреть логи
```
PS C:\Windows\system32> create deployment nginx --namespace default --image=nginx:latest --replicas=2
deployment.apps/hello-world created
PS C:\Windows\system32> kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
nginx-654975c8cd-4gqv6   1/1     Running   0          16s
nginx-654975c8cd-8m8vv   1/1     Running   0          16s
PS C:\Windows\system32> kubectl get deployment
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   2/2     2            2           89s
```
## Задание 2: Просмотр логов для разработки
```
PS C:\Windows\system32> kubectl config use-context developer
Switched to context "developer".
PS C:\Windows\system32> kubectl get pods -n default
Error from server (Forbidden): pods is forbidden: User "developer" cannot list resource "pods" in API group "" in the namespace "default"
PS C:\Windows\system32> kubectl config use-context minikube
Switched to context "minikube".
PS C:\Windows\system32> kubectl get pods -n default
NAME                     READY   STATUS    RESTARTS   AGE
nginx-654975c8cd-4gqv6   1/1     Running   0          16s
nginx-654975c8cd-8m8vv   1/1     Running   0          16s
```

## Задание 3: Изменение количества реплик 
```
PS D:\Projects\devkub-homeworks\12-kubernetes-02-commands> kubectl apply -f deployment.yml
deployment.apps/nginx configured
PS D:\Projects\devkub-homeworks\12-kubernetes-02-commands> kubectl get deployments
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   5/5     5            5           22m
PS D:\Projects\devkub-homeworks\12-kubernetes-02-commands> kubectl get pods
NAME                    READY   STATUS    RESTARTS   AGE
nginx-8656494f4-7ncpq   1/1     Running   0          75s
nginx-8656494f4-92tw9   1/1     Running   0          75s
nginx-8656494f4-kdb8z   1/1     Running   0          41s
nginx-8656494f4-nf4mv   1/1     Running   0          75s
nginx-8656494f4-xh8hg   1/1     Running   0          32s
```
