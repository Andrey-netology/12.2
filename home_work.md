1. Запуск пода из образа в деплойменте

Вначале становил kubelet и kubeadm (kubectl установил в прошлом ДЗ) 


root@kuber1:/home/admin/dev#  kubectl apply -f nginx-deployment.yaml
deployment.apps/nginx-deployment created

root@kuber1:/home/admin/dev# kubectl apply -f nginx-hello.yaml
deployment.apps/nginx-hello created

Скрин положил отдельно в репозиторий 

2. Просмотр логов для разработки

Скрин положил отдельно в репозиторий 

Просмотр логов: 

Скрин положил отдельно в репозиторий 



3. Изменение количества реплик

root@kuber1:/home/admin/dev# kubectl apply -f nginx-hello.yaml
deployment.apps/nginx-hello configured

Скрин положил отдельно в репозиторий 
