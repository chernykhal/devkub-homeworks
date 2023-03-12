# Решение домашнего задания к занятию "13.1 контейнеры, поды, deployment, statefulset, services, endpoints"

## Задание 1: подготовить тестовый конфиг для запуска приложения
```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: front-back
  name: front-back
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: front-back
  template:
    metadata:
      labels:
        app: front-back
    spec:
      containers:
        - image: nginx
          imagePullPolicy: IfNotPresent
          name: front
        - image: praqma/network-multitool
          imagePullPolicy: IfNotPresent
          name: back
          env:
          - name: HTTP_PORT
            value: "88"


---
apiVersion: v1
kind: Service
metadata:
  name: front-back
  namespace: default
spec:
  ports:
    - name: front
      port: 80
    - name: back
      port: 88
  selector:
    app: front-back
```
Результат:
```
a.chernyh@srv-cl-master-1:/home/manifests$ sudo kubectl get all
NAME                              READY   STATUS    RESTARTS   AGE
pod/front-back-5f7cff64c6-5brmp   2/2     Running   0          65s
pod/postgres-0                    1/1     Running   0          52s

NAME                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/front-back   ClusterIP   10.233.33.26    <none>        80/TCP,88/TCP    65s
service/kubernetes   ClusterIP   10.233.0.1      <none>        443/TCP          3h9m
service/postgres     NodePort    10.233.17.183   <none>        5432:30933/TCP   53s

NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/front-back   1/1     1            1           65s

NAME                                    DESIRED   CURRENT   READY   AGE
replicaset.apps/front-back-5f7cff64c6   1         1         1       65s

NAME                        READY   AGE
statefulset.apps/postgres   1/1     53s
```
## Задание 2: подготовить конфиг для production окружения
frontend:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: front
  name: front
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: front
  template:
    metadata:
      labels:
        app: front
    spec:
      containers:
        - image: praqma/network-multitool
          imagePullPolicy: IfNotPresent
          name: front
          env:
          - name: BACKEND_ADDR
            value: back
---
apiVersion: v1
kind: Service
metadata:
  name: front
  namespace: default
spec:
  ports:
    - name: front
      port: 80
  selector:
    app: front
```
backend:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: back
  name: back
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: back
  template:
    metadata:
      labels:
        app: back
    spec:
      containers:
        - image: praqma/network-multitool
          imagePullPolicy: IfNotPresent
          name: back
          env:
          - name: DB_ADDR
            value: postgres      
---
apiVersion: v1
kind: Service
metadata:
  name: back
  namespace: default
spec:
  ports:
    - name: back
      port: 80
  selector:
    app: back
```

Результат:
```
a.chernyh@srv-cl-master-1:/home/manifests$ sudo kubectl get all
NAME                              READY   STATUS    RESTARTS   AGE
pod/back-697f47db6f-nxhkv         1/1     Running   0          12s
pod/front-back-5f7cff64c6-5brmp   2/2     Running   0          6m14s
pod/front-cdb4f9c79-kdl6r         1/1     Running   0          7s
pod/postgres-0                    1/1     Running   0          6m1s

NAME                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/back         ClusterIP   10.233.4.168    <none>        80/TCP           12s
service/front        ClusterIP   10.233.31.102   <none>        80/TCP           7s
service/front-back   ClusterIP   10.233.33.26    <none>        80/TCP,88/TCP    6m14s
service/kubernetes   ClusterIP   10.233.0.1      <none>        443/TCP          3h14m
service/postgres     NodePort    10.233.17.183   <none>        5432:30933/TCP   6m2s

NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/back         1/1     1            1           12s
deployment.apps/front        1/1     1            1           7s
deployment.apps/front-back   1/1     1            1           6m14s

NAME                                    DESIRED   CURRENT   READY   AGE
replicaset.apps/back-697f47db6f         1         1         1       12s
replicaset.apps/front-back-5f7cff64c6   1         1         1       6m14s
replicaset.apps/front-cdb4f9c79         1         1         1       7s

NAME                        READY   AGE
statefulset.apps/postgres   1/1     6m2s
```
