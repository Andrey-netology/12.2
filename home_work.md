1. Запуск пода из образа в деплойменте

Вначале установил kubelet и kubeadm (kubectl установил в прошлом ДЗ) 


root@kuber1:/home/admin/dev#  kubectl apply -f nginx-deployment.yaml
deployment.apps/nginx-deployment created

root@kuber1:/home/admin/dev# kubectl apply -f nginx-hello.yaml
deployment.apps/nginx-hello created

root@kuber1:/home/admin/dev# kubectl get deployment

| NAME             | Ready   | UP-TO-DATE  | AVAILABLE | AGE   |
| ---------------- |:-------:| :----------:|:---------:|------:|
| hello-node       | 1/1     | 1           | 1         | 163m  |
| nginx-deployment | 2/2     | 2           | 2         | 23m   |
| nginx-hello      | 2/2     | 2           | 2         | 6m56s |

root@kuber1:/home/admin/dev#  kubectl get pods

| NAME                              | Ready   | STATUS      | RESTARTS  | AGE   |
| --------------------------------- |:-------:| :----------:|:---------:|------:|
| hello-node-6b89d599b9-55j8b       | 1/1     | Running     | 0         | 164m  |
| nginx-deployment-9456bbbf9-nqzc8  | 2/2     | Running     | 0         | 23m   |
| nginx-deployment-9456bbbf9-tcbb7  | 2/2     | Running     | 0         | 23m   |
| nginx-hello-9456bbbf9-c9pp8       | 2/2     | Running     | 0         | 7m9s  |
| nginx-hello-9456bbbf9-zp4th       | 2/2     | Running     | 0         | 7m9s  |

2. Просмотр логов для разработки

Создал пользователя через готовый скрипт https://github.com/robertwalid/K8s_User_Creation_X509_Certs: 
![alt text](https://github.com/Andrey-netology/12.2/blob/main/kuber1.JPG "Logo Title Text 1")

Конфиг:
![alt text](https://github.com/Andrey-netology/12.2/blob/main/kuber2.JPG "Logo Title Text 1")

Назначение прав:
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: Werg
  namespace: nginx-hello
subjects:
- kind: User
  name: Werg
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: edit
  apiGroup: rbac.authorization.k8s.io
---------------------------------
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: Werg
  namespace: nginx-hello
subjects:
- kind: User
  name: Werg
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: view
  apiGroup: rbac.authorization.k8s.io

Логи: 
![alt text](https://github.com/Andrey-netology/12.2/blob/main/2.2.JPG "Logo Title Text 1")

POD: 
![alt text](https://github.com/Andrey-netology/12.2/blob/main/2.3.JPG "Logo Title Text 1")

3. Изменение количества реплик

root@kuber1:/home/admin/dev# kubectl apply -f nginx-hello.yaml
deployment.apps/nginx-hello configured

Реплики: 
![alt text](https://github.com/Andrey-netology/12.2/blob/main/3.1.JPG "Logo Title Text 1")

