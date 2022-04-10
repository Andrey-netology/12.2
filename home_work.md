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

Конфиг: 
root@kuber1:~/.kube# kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority: /root/.minikube/ca.crt
    extensions:
    - extension:
        last-update: Fri, 08 Apr 2022 09:06:36 UTC
        provider: minikube.sigs.k8s.io
        version: v1.25.2
      name: cluster_info
    server: https://10.128.0.20:8443
  name: minikube
contexts:
- context:
    cluster: minikube
    extensions:
    - extension:
        last-update: Fri, 08 Apr 2022 09:06:36 UTC
        provider: minikube.sigs.k8s.io
        version: v1.25.2
      name: context_info
    namespace: default
    user: minikube
  name: minikube
current-context: minikube
kind: Config
preferences: {}
users:
- name: minikube
  user:
    client-certificate: /root/.minikube/profiles/minikube/client.crt
    client-key: /root/.minikube/profiles/minikube/client.key
- name: test
  user:
    token: REDACTED
Просмотр логов: 

Скрин положил отдельно в репозиторий 



3. Изменение количества реплик

root@kuber1:/home/admin/dev# kubectl apply -f nginx-hello.yaml
deployment.apps/nginx-hello configured

Скрин положил отдельно в репозиторий 
