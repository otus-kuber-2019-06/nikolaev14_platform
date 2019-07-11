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
