### nikolaev14_platform
nikolaev14 Platform repository

### Homework-1
#### Установка kubectl

	$brew install kubernetes-cli
>>>
	$kubectl version
>>>
    Client Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.0", GitCommit:"e8462b5b5dc2584fdcd18e6bcfe9f1e4d970a529", GitTreeState:"clean", BuildDate:"2019-06-20T04:49:16Z", GoVersion:"go1.12.6", Compiler:"gc", Platform:"darwin/amd64"}

#### Добавление autocompletion

Использую oh-my-zsh, достаточно добавить плагин в .zshrc
Попутно поделюсь своими плагинами:
    plugins=(git minikube kubectl ansible cp dash docker emoji git-flow go gradle helm history iterm2 jira npm pip python screen themes tig vault vim-interaction vscode zsh-navigation-tools kube-ps1)

#### Установка minikube

	$brew install minikube virtualbox

#### Запуск minikube

	$minikube start
>>>
    😄  minikube v1.2.0 on darwin (amd64)
    💡  Tip: Use 'minikube start -p <name>' to create a new cluster, or 'minikube delete' to delete this one.
    🔄  Restarting existing virtualbox VM for "minikube" ...
    ⌛  Waiting for SSH access ...
    🐳  Configuring environment for Kubernetes v1.15.0 on Docker 18.09.6
    🔄  Relaunching Kubernetes v1.15.0 using kubeadm ...
    ⌛  Verifying: apiserver proxy etcd scheduler controller dns
    🏄  Done! kubectl is now configured to use "minikube"

	$minikube status
>>>
    host: Running
    kubelet: Running
    apiserver: Running
    kubectl: Correctly Configured: pointing to minikube-vm at 192.168.99.100
>>>
	$kubectl config view
>>>
    apiVersion: v1
    clusters:
    - cluster:
        certificate-authority: /Users/igor/.minikube/ca.crt
        server: https://192.168.99.100:8443
    name: minikube
    contexts:
    - context:
        cluster: minikube
        user: minikube
    name: minikube
    current-context: minikube
    kind: Config
    preferences: {}
    users:
    - name: minikube
    user:
        client-certificate: /Users/igor/.minikube/client.crt
        client-key: /Users/igor/.minikube/client.key
>>>
	$kubectl cluster-info
>>>
    Kubernetes master is running at https://192.168.99.100:8443
    KubeDNS is running at https://192.168.99.100:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

#### Посмотрим на k9s
Поставил из brew, штука забавная и полезная берем в пользование.


#### Запускаем Dashboard
>>>
	$minikube addons enable dashboard
	$minikube dashboard
>>>
    🤔  Verifying dashboard health ...
    🚀  Launching proxy ...
    🤔  Verifying proxy health ...
    🎉  Opening http://127.0.0.1:60216/api/v1/namespaces/kube-system/services/http:kubernetes-dashboard:/proxy/ in your default browser...

#### Смотрим, что там внутри виртуалки с minikube

	$minikube ssh
>>>
                             _             _
                _         _ ( )           ( )
      ___ ___  (_)  ___  (_)| |/')  _   _ | |_      __
    /' _ ` _ `\| |/' _ `\| || , <  ( ) ( )| '_`\  /'__`\
    | ( ) ( ) || || ( ) || || |\`\ | (_) || |_) )(  ___/
    (_) (_) (_)(_)(_) (_)(_)(_) (_)`\___/'(_,__/'`\____)

	$docker ps
    Большой вывод по запущенным контейнерам
>>>
	$docker rm -f $(docker ps -a -q)
>>>
    ...
    5579729a60c9
    2b21876e2c8c
    611a42222f48
    ...

Удолил, ты все удолил...
Но все вернулось, а почему?

#### Экспериментируем с kubectl

	$kubectl get pods -n kube-system
>>>
    NAME                                    READY   STATUS    RESTARTS   AGE
    coredns-5c98db65d4-k9r2d                1/1     Running   0          34h
    coredns-5c98db65d4-pv7q9                1/1     Running   0          34h
    etcd-minikube                           1/1     Running   0          34h
    kube-addon-manager-minikube             1/1     Running   0          34h
    kube-apiserver-minikube                 1/1     Running   0          34h
    kube-controller-manager-minikube        1/1     Running   0          34h
    kube-proxy-ftw85                        1/1     Running   0          34h
    kube-scheduler-minikube                 1/1     Running   0          34h
    kubernetes-dashboard-7b8ddcb5d6-k8mpt   1/1     Running   0          34h
    storage-provisioner                     1/1     Running   0          34h
>>>
	$kubectl delete pod --all -n kube-system
>>>
    pod "coredns-5c98db65d4-k9r2d" deleted
    pod "coredns-5c98db65d4-pv7q9" deleted
    pod "etcd-minikube" deleted
    pod "kube-addon-manager-minikube" deleted
    pod "kube-apiserver-minikube" deleted
    pod "kube-controller-manager-minikube" deleted
    pod "kube-proxy-ftw85" deleted
    pod "kube-scheduler-minikube" deleted
    pod "kubernetes-dashboard-7b8ddcb5d6-k8mpt" deleted
    pod "storage-provisioner" deleted
>>>
	$kubectl get componentstatuses #Сокращенно kubectl get cs
>>>
    NAME                 STATUS    MESSAGE             ERROR
    controller-manager   Healthy   ok
    scheduler            Healthy   ok
    etcd-0               Healthy   {"health":"true"}


### Ответ на домашнее задание

	$kubectl get pods -n kube-system
>>>
	NAME                                    READY   STATUS    RESTARTS   AGE
	coredns-5c98db65d4-9bmdg                1/1     Running   0          41m
	coredns-5c98db65d4-htwcv                1/1     Running   0          41m
	etcd-minikube                           1/1     Running   0          40m
	kube-addon-manager-minikube             1/1     Running   0          41m
	kube-apiserver-minikube                 1/1     Running   0          41m
	kube-controller-manager-minikube        1/1     Running   0          41m
	kube-proxy-kjxpz                        1/1     Running   0          40m
	kube-scheduler-minikube                 1/1     Running   0          40m
	kubernetes-dashboard-7b8ddcb5d6-j7zjh   1/1     Running   0          41m
	storage-provisioner                     1/1     Running   0          40m

#### coredns

	$kubectl -n kube-system describe replicasets coredns
>>>
	Annotations:    deployment.kubernetes.io/desired-replicas: 2
	                deployment.kubernetes.io/max-replicas: 3
	                deployment.kubernetes.io/revision: 1
	Controlled By:  Deployment/coredns
	Replicas:       2 current / 2 desired
	Pods Status:    2 Running / 0 Waiting / 0 Succeeded / 0 Failed

#### kube-apiserver
	
	$ ps -eo 'tty,pid,comm' | grep ^? | grep api
	?3584 kube-apiserver

	$ ps -eo 'tty,pid,comm' | grep ^? | grep kubelet
	?9917 kubelet

#### kubelet stop

	$sudo systemctl stop kubelet
	$kubectl -n kube-system get pods
>>>
	NAME                                    READY   STATUS        RESTARTS   AGE
	coredns-5c98db65d4-8qlc2                1/1     Terminating   0          12m
	coredns-5c98db65d4-bb97z                1/1     Terminating   0          12m
	coredns-5c98db65d4-f2ttt                0/1     Pending       0          19s
	coredns-5c98db65d4-lkljs                0/1     Pending       0          19s
	etcd-minikube                           1/1     Terminating   0          12m
	kube-addon-manager-minikube             1/1     Terminating   0          11m
	kube-apiserver-minikube                 1/1     Terminating   0          11m
	kube-controller-manager-minikube        1/1     Terminating   0          12m
	kube-proxy-fzx4m                        1/1     Terminating   0          12m
	kube-scheduler-minikube                 1/1     Terminating   0          11m
>>>
	$sudo systemctl start kubelet
	$kubectl -n kube-system get pods
>>>
	NAME                                    READY   STATUS    RESTARTS   AGE
	coredns-5c98db65d4-f2ttt                0/1     Pending   0          75s
	coredns-5c98db65d4-lkljs                0/1     Pending   0          75s
	etcd-minikube                           1/1     Running   0          12s
	kube-addon-manager-minikube             1/1     Running   0          12s
	kube-apiserver-minikube                 1/1     Running   0          10s
	kube-controller-manager-minikube        1/1     Running   0          12s
	kube-proxy-f2zjk                        0/1     Pending   0          3s
	kube-scheduler-minikube                 1/1     Running   0          9s
	kubernetes-dashboard-7b8ddcb5d6-9jnnq   0/1     Pending   0          75s

Вывод - с погашенным kubelet поды продолжали работать, однако, по всей видимости, кластер
    должен был развалиться.
coredns - имеет replikaset с 2мя репликами, потому и поддерживает их количество 
kube-apiserver и kubelet - системные сервисы и их работа поддерживается ОС


### Homework-2 Безопасность в Kubernetes.

#### task01
Создан sa bob с ролью admin для всего кластера.
Создан sa пользователя dave без доступа.

#### task02
Создан ns prometheus.
Создан sa carol в ns prometheus.
Для всех sa в ns prometheus предоставлены разрешения на [ get, list, watch ] для podов всего кластера.

#### task03
Создан ns dev
Создан sa jane в ns dev
Предоставлены привелении admin для jane в ns dev
Создан sa ken в ns dev
Предоставлены привелегии view для ken в ns dev

