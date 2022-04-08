1. Запуск пода из образа в деплойменте

Вначале становил kubelet и kubeadm (kubectl установил в прошлом ДЗ) 


root@kuber1:/home/admin/dev#  kubectl apply -f nginx-deployment.yaml
deployment.apps/nginx-deployment created

root@kuber1:/home/admin/dev# kubectl apply -f nginx-hello.yaml
deployment.apps/nginx-hello created

root@kuber1:/home/admin/dev# kubectl get deployment
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
hello-node         1/1     1            1           163m
nginx-deployment   2/2     2            2           23m
nginx-hello        2/2     2            2           6m56s
root@kuber1:/home/admin/dev#  kubectl get pods
NAME                               READY   STATUS    RESTARTS   AGE
hello-node-6b89d599b9-55j8b        1/1     Running   0          164m
nginx-deployment-9456bbbf9-nqzc8   1/1     Running   0          23m
nginx-deployment-9456bbbf9-tcbb7   1/1     Running   0          23m
nginx-hello-9456bbbf9-c9pp8        1/1     Running   0          7m9s
nginx-hello-9456bbbf9-zp4th        1/1     Running   0          7m9s

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

root@kuber1:~/.kube# kubectl logs hello-node-6b89d599b9-55j8b
172.17.0.1 - - [08/Apr/2022:09:57:50 +0000] "\x16\x03\x01\x02\x00\x01\x00\x01\xFC\x03\x03b\x170\x99\x5Cp\xAC\x02\xD3\x1F~\xD6\x16`Lw\xCC1\xDE7\x1F\x82|\x19\xFA\x9E\xD88\xF0\xF6\xBF\xB5 d\xB5\xF0\xE8\xA8576l\x163\xB0\xBBJ\xB4Tw6 \xE8m\xAD\x1A\xA6\xCB\xACD\x0Er\xFEU\x8F\x00 \xFA\xFA\x13\x01\x13\x02\x13\x03\xC0+\xC0/\xC0,\xC00\xCC\xA9\xCC\xA8\xC0\x13\xC0\x14\x00\x9C\x00\x9D\x00/\x005\x01\x00\x01\x93**\x00\x00\x00\x17\x00\x00\xFF\x01\x00\x01\x00\x00" 400 173 "-" "-"
172.17.0.1 - - [08/Apr/2022:09:57:50 +0000] "\x16\x03\x01\x02\x00\x01\x00\x01\xFC\x03\x03\x01$\x10\x1E\x81\xC3I\x18E\xAAy\xB4t\x05\xD6\x96\xC0\x92\xAD\xE7W\xB5\x03cq\xEDM\xB4\xFB\xAEF\xB0 \xFF\xD3\xC3\xEEO&B\x9E\x18\x8A\x1FFY\x14\xA8\xA0e\xBDE\x9C\x99\x86\x7F\x89\x03@\xD5\xB4@\xB2\x9Aw\x00 ::\x13\x01\x13\x02\x13\x03\xC0+\xC0/\xC0,\xC00\xCC\xA9\xCC\xA8\xC0\x13\xC0\x14\x00\x9C\x00\x9D\x00/\x005\x01\x00\x01\x93**\x00\x00\x00\x17\x00\x00\xFF\x01\x00\x01\x00\x00" 400 173 "-" "-"
172.17.0.1 - - [08/Apr/2022:09:58:05 +0000] "GET / HTTP/1.1" 200 785 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.75 Safari/537.36"
172.17.0.1 - - [08/Apr/2022:09:58:05 +0000] "GET /favicon.ico HTTP/1.1" 200 744 "http://51.250.79.80:31211/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.75 Safari/537.36"
172.17.0.1 - - [08/Apr/2022:10:04:44 +0000] "GET / HTTP/1.1" 200 785 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.75 Safari/537.36"
172.17.0.1 - - [08/Apr/2022:10:04:45 +0000] "GET /favicon.ico HTTP/1.1" 200 744 "http://51.250.79.80:31211/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.75 Safari/537.36"


root@kuber1:~/.kube# kubectl describe pod hello-node-6b89d599b9-55j8b
Name:         hello-node-6b89d599b9-55j8b
Namespace:    default
Priority:     0
Node:         kuber1/10.128.0.20
Start Time:   Fri, 08 Apr 2022 09:45:37 +0000
Labels:       app=hello-node
              pod-template-hash=6b89d599b9
Annotations:  <none>
Status:       Running
IP:           172.17.0.6
IPs:
  IP:           172.17.0.6
Controlled By:  ReplicaSet/hello-node-6b89d599b9
Containers:
  echoserver:
    Container ID:   docker://23ba12cf7cda6d1d2032434245bafff4a84ef479e7b455d0e1d5cd4148c347bd
    Image:          k8s.gcr.io/echoserver:1.4
    Image ID:       docker-pullable://k8s.gcr.io/echoserver@sha256:5d99aa1120524c801bc8c1a7077e8f5ec122ba16b6dda1a5d3826057f67b9bcb
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Fri, 08 Apr 2022 09:45:44 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-9xln8 (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  kube-api-access-9xln8:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s                   
Events:
  Type    Reason          Age   From     Message
  ----    ------          ----  ----     -------
  Normal  SandboxChanged  34m   kubelet  Pod sandbox changed, it will be killed and re-created.
  Normal  Pulled          33m   kubelet  Container image "k8s.gcr.io/echoserver:1.4" already present on machine
  Normal  Created         33m   kubelet  Created container echoserver
  Normal  Started         33m   kubelet  Started container echoserver

3. Изменение количества реплик

root@kuber1:/home/admin/dev# kubectl apply -f nginx-hello.yaml
deployment.apps/nginx-hello configured

root@kuber1:/home/admin/dev# kubectl get pods
NAME                               READY   STATUS    RESTARTS   AGE
hello-node-6b89d599b9-55j8b        1/1     Running   0          3h54m
nginx-deployment-9456bbbf9-nqzc8   1/1     Running   0          93m
nginx-deployment-9456bbbf9-tcbb7   1/1     Running   0          93m
nginx-hello-9456bbbf9-c9pp8        1/1     Running   0          77m
nginx-hello-9456bbbf9-fnq2x        1/1     Running   0          22s
nginx-hello-9456bbbf9-nc7hm        1/1     Running   0          22s
nginx-hello-9456bbbf9-qz9pl        1/1     Running   0          22s
nginx-hello-9456bbbf9-zp4th        1/1     Running   0          77m
