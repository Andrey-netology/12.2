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

Скрин положил отдельно в репозиторий 

Просмотр логов: 

Скрин положил отдельно в репозиторий 



3. Изменение количества реплик

root@kuber1:/home/admin/dev# kubectl apply -f nginx-hello.yaml
deployment.apps/nginx-hello configured

Скрин положил отдельно в репозиторий 
