1. Запуск пода из образа в деплойменте

Вначале установил kubelet и kubeadm (kubectl установил в прошлом ДЗ) 


root@kuber1:/home/admin/dev#  kubectl apply -f nginx-deployment.yaml
deployment.apps/nginx-deployment created

root@kuber1:/home/admin/dev# kubectl apply -f nginx-hello.yaml
deployment.apps/nginx-hello created

| NAME             | Ready   | UP-TO-DATE  | AVAILABLE | AGE   |
| ---------------- |:-------:| :----------:|:---------:|------:|
| hello-node       | 1/1     | 1           | 1         | 163m  |
| nginx-deployment | 2/2     | 2           | 2         | 23m   |
| nginx-hello      | 2/2     | 2           | 2         | 6m56s |

2. Просмотр логов для разработки

Скрин положил отдельно в репозиторий 

Просмотр логов: 

Скрин положил отдельно в репозиторий 



3. Изменение количества реплик

root@kuber1:/home/admin/dev# kubectl apply -f nginx-hello.yaml
deployment.apps/nginx-hello configured

Скрин положил отдельно в репозиторий 
