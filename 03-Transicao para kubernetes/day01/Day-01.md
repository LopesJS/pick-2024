# Transição para o Kubernetes - Day 01:

### Comandos Básicos do Kubernetes:
```
kubectl get nodes
```
```
kubectl get pods (po)
```
```
kubectl get service (svc)
```
```
kubectl get deployment (deplo)
```
```
kubectlget replicaset 
```

### Pods do sistema do kubernetes (-n = namespace):
```
kubectl get pods -n kube-system
```

### Maiores informações na consulta (como IP e node):
```
kubectl get pods -n kube-system -o wide
```

### Todos os pods do cluster (-A = all):
```
kubectl get pods -A 
```


### Auto complete:

* Instalar o bash-completion:
```
apt install bash-completion
```

* Habilitar o completion do kubectl

* Ajuda:
```
kubectl completion --help
```

* Rodar um nginx:
```
kubectl run --image nginx --port 80
```

* Executar o bash no pod do Nginx:
```
kubectl exec -ti nome-do-pod -- bash
```

* Sair do pod:
```
exit
```

* Deletar o pod:
```
kubectl delete pods nome-do-pod
```

* Criar Alias:
```
alias k=kubectl
```

* Configurar alias
vim /root/.bash_profile e inserir alias k="kubectl"

* Exemplo do comando usando alias:
```
k get pods
```

* Criar um serviço NodePort para expor um pod:
```
kubectl expose pods nome-do-pod --type NodePort
```

* Deletar o serviço:
```
kubectl delete service nome-do-servico
```

* kubectl com dry-run: 
```
# Gera em tela definições em yaml com as informações no comando:
kubectl run --image nginx --port 80 nome-do-pod --dry-run=client -o yaml
```

```
# Gera arquivo em yaml com as informações no comando:
kubectl run --image nginx --port 80 meu-primeiro-pod --dry-run=client -o yaml > pod.yaml
```


### Referências:
https://kubernetes.io/pt-br/docs/tasks/tools/install-kubectl-linux/
