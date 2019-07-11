### nikolaev14_platform
nikolaev14 Platform repository


#### Установка kubectl

	$brew install kubernetes-cli

	$kubectl version
>>>
    Client Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.0", GitCommit:"e8462b5b5dc2584fdcd18e6bcfe9f1e4d970a529", GitTreeState:"clean", BuildDate:"2019-06-20T04:49:16Z", GoVersion:"go1.12.6", Compiler:"gc", Platform:"darwin/amd64"}

#### Добавление autocompletion

Использую oh-my-zsh, достаточно добавить плагин в .zshrc
Попутно поделюсь своими плагинами:
    plugins=(git minikube kubectl ansible cp dash docker emoji git-flow go gradle helm history iterm2 jira npm pip python screen themes tig vault vim-interaction vscode zsh-navigation-tools)

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

	$kubectl cluster-info
>>>
    Kubernetes master is running at https://192.168.99.100:8443
    KubeDNS is running at https://192.168.99.100:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

#### Посмотрим на k9s
Поставил из brew, штука забавная и полезная берем в пользование.


#### Запускаем Dashboard

	$minikube addons enable dashboard
	$minikube dashboard
>>>
    🤔  Verifying dashboard health ...
    🚀  Launching proxy ...
    🤔  Verifying proxy health ...
    🎉  Opening http://127.0.0.1:60216/api/v1/namespaces/kube-system/services/http:kubernetes-dashboard:/proxy/ in your default browser...


