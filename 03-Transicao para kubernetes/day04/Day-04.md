# Day-04

### ReplicaSets:

Cria e gerencia as réplicas de pods expecificada no Deployment. O Deployment é um objeto que cria um ReplicaSet, e o ReplicaSet é um objeto que cria um pod.
Ao criar um deployment, o replicaset é criado automaticamente, e é o replicaset que vai criar os pods que estão dentro do deployment.

* Para fazer o rollback para a versão anterior de um Deployment:
```
kubectl rollout undo deployment nome-do-deployment
```

### DaemonSets:

É um objeto que cria um pod que fica rodando em todos os nodes do cluster, garantindo que pelo menos um pod esteja rodando em cada node do cluster.

Exemplo de criação um daemonset que vai garantir que todos os nós do cluster executem uma réplica do pod "node-exporter", um exporter de métricas do Prometheus.

1. Criar o arquivo node-exporter-daemonset.yaml;

2. Imputar as informações no arquivo;

3. Criar o DaemonSet utilizando o arquivo de manifesto:
```
kubectl apply -f node-exporter-daemonset.yaml
```

4. Verificar a criação do DaemonSet:
```
kubectl get daemonset
```

5. Para Verificar os pods que o DaemonSet está gerenciando:
```
kubectl get pods -l app=node-exporter 
```
_O parâmetro "-l" é um filtro para a label expecificada no manifesto._


6. Verificar se os pods do node-exporter estão sendo executados em todos os nós do cluster:
```
kubectl get pods -o wide -l app=node-exporter
```

7. Verificar os detalhes do DaemonSet:
   
```
kubectl describe daemonset node-exporter
```


## Observação:
Daemonset e replicaset não são possíveis criá-los via comando "kubectl create..." somente via arquivos manifesto.


### Probes:

As probes são uma forma de você monitorar o seu Pod e saber se ele está em um estado saudável ou não. 
Com elas é possível assegurar que seus Pods estão rodando e respondendo de maneira correta, e mais do que isso, que o Kubernetes está testando o que está sendo executado dentro do seu Pod.

Atualmente há três tipos de probes, a livenessProbe, a readinessProbe e a startupProbe. 

**Liveness Probe:**

A livenessProbe é a probe de verificação de integridade, verificando se o que está rodando dentro do Pod está saudável. Sendo uma forma de testar se o que temos dentro do Pod está respondendo conforme esperado. Se por acaso o teste falhar, o Pod será reiniciado.

```
        livenessProbe: # Aqui é onde vamos adicionar a nossa livenessProbe
          httpGet: # Aqui vamos utilizar o httpGet, onde vamos se conectar ao container através do protocolo HTTP
            path: / # Qual o endpoint que vamos utilizar para se conectar ao container
            port: 80 # Qual porta TCP vamos utilizar para se conectar ao container
          initialDelaySeconds: 10 # Quantos segundos vamos esperar para executar a primeira verificação
          periodSeconds: 10 # A cada quantos segundos vamos executar a verificação
          timeoutSeconds: 5 # Quantos segundos vamos esperar para considerar que a verificação falhou
          failureThreshold: 3 # Quantos falhas consecutivas vamos aceitar antes de reiniciar o container
```

**Readiness Probe:**

A readinessProbe é uma forma do Kubernetes verificar se o seu container está pronto para receber tráfego, se ele está pronto para receber requisições vindas de fora.
É a probe de leitura, e fica verificando se o nosso container está pronto para receber requisições, e se estiver pronto, ele irá receber requisições, caso contrário, ele não irá receber requisições, pois será removido do endpoint do serviço, fazendo com que o tráfego não chegue até ele. Ela garante que o Pod está saudável para receber requisições.


```
        readinessProbe: # Onde definimos a nossa probe de leitura
          httpGet: # O tipo de teste que iremos executar, neste caso, iremos executar um teste HTTP
            path: / # O caminho que iremos testar
            port: 80 # A porta que iremos testar
          initialDelaySeconds: 10 # O tempo que iremos esperar para executar a primeira vez a probe
          periodSeconds: 10 # De quanto em quanto tempo iremos executar a probe
          timeoutSeconds: 5 # O tempo que iremos esperar para considerar que a probe falhou
          successThreshold: 2 # O número de vezes que a probe precisa passar para considerar que o container está pronto
          failureThreshold: 3 # O número de vezes que a probe precisa falhar para considerar que o container não está pronto
```


**Startup Probe:**

Uma das probes menos utilizada, mas muito importante. Ela é a responsável por verificar se o nosso container foi inicializado corretamente, e se ele está pronto para receber requisições.
Muito parecido com a readinessProbe, mas a diferença é que a startupProbe é executada apenas uma vez no começo da vida do nosso container, e a readinessProbe é executada de tempos em tempos.

```
        startupProbe: # Onde definimos a nossa probe de inicialização
          httpGet: # O tipo de teste que iremos executar, neste caso, iremos executar um teste HTTP
            path: / # O caminho que iremos testar
            port: 80 # A porta que iremos testar
          initialDelaySeconds: 10 # O tempo que iremos esperar para executar a primeira vez a probe
          periodSeconds: 10 # De quanto em quanto tempo iremos executar a probe
          timeoutSeconds: 5 # O tempo que iremos esperar para considerar que a probe falhou
          successThreshold: 2 # O número de vezes que a probe precisa passar para considerar que o container está pronto
          failureThreshold: 3 # O número de vezes que a probe precisa falhar para considerar que o container não está pronto
```


### Referência:
https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/ 
