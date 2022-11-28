# Probes
***
## O que são?
***
* Probes são "Provas de Vida"  de um container, então no caso de um probe Liveness por exemplo, o kubernets vai enviar "testes de atividade" para saber quando dar um restart no container e reiniciá-lo em tal estado.
* O kubelet usa testes de prontidão para saber quando um contêiner está pronto para começar a aceitar tráfego. Um Pod é considerado pronto quando todos os seus contêineres estão prontos. Um uso desse sinal é controlar quais pods são usados ​​como back-end para serviços. Quando um pod não está pronto, ele é removido dos balanceadores de carga de serviço.
* Os probes podem ser definidos dentro do arquivo de criação do pod.
* Existem 3 tipos de Probes:
  * Liveness
  * Readiness
  * Startup Probes
***
### Liveness Probe
***
* A liveness probe é usada para determinar se o contêiner está funcionando. 
* Se o kubelet não receber uma resposta de liveness probe de um contêiner, ele mata o contêiner e o contêiner é reiniciado de acordo com a sua política de reinicialização.
*  Se uma liveness probe for definida para um contêiner, o kubelet executa a liveness probe periodicamente (segundo o intervalo especificado) e mata o contêiner se a liveness probe falhar. Se o contêiner estiver morto, o kubelet o reinicia.
* Exemplo de liveness probe:
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    test: liveness
  name: liveness-http
spec:
  containers:
  - name: liveness
    image: registry.k8s.io/liveness
    ports:
    - containerPort: 8080
    args:
    - /server
    livenessProbe:
      httpGet:
        path: /healthz ("Endpoint que será chamado para verificar se o container está vivo")
        port: 8080
        httpHeaders:
        - name: Custom-Header
          value: Awesome
      initialDelaySeconds: 20 #tempo de espera para o container iniciar e começar a verificar se está vivo
      periodSeconds: 3 #De quanto em quanto tempo o container vai verificar se está vivo
      failureThreshold: 3 #Quantidade de falhas que o container pode ter antes de ser reiniciado
```
***
## Readiness Probe
***
* A readiness probe é usada para determinar se o contêiner está pronto para aceitar tráfego ("Requisições").
* Um pod com contêineres informando que não estão prontos não recebe tráfego por meio do Kubernetes Services.
* Readiness probes são configurados de forma semelhante a liveness probes, mudando apenas o campo `readinessProbe` no arquivo de criação do pod ao invés do `livenessProbe`.
* Outra diferença é que o kubelet não mata o contêiner e não reinicia o contêiner se a readiness probe falhar. O contêiner permanece no estado atual e não é marcado como pronto.
* Exemplo de readiness probe:
```yaml
readinessProbe:
      httpGet:
        path: /healthz ("Endpoint que será chamado para verificar se o container está vivo")
        port: 8080
        httpHeaders:
        - name: Custom-Header
          value: Awesome
      initialDelaySeconds: 20 #tempo de espera para o container iniciar e começar a verificar se o container está pronto
      periodSeconds: 3 #De quanto em quanto tempo o container vai verificar se o container está pronto para receber requisições
      failureThreshold: 3 #Quantidade de falhas que o container pode ter antes de enviar as requisições mesmo falhando
```
## Startup Probe
*** 
* Algumas aplicações legadas não podem suportar liveness probes porque elas não iniciam rapidamente o suficiente e podem levar muito tempo para se inicializarem. Nesses casos, você pode usar uma startup probe para determinar se a aplicação foi iniciada.
* O truque é configurar uma sondagem de inicialização com o mesmo comando, verificação de HTTP ou TCP, com `failureThreshold * periodSeconds` tempo suficiente para cobrir o tempo de inicialização do pior caso.
```yaml
startupProbe:
  httpGet:
    path: /healthz
    port: liveness-port
  failureThreshold: 30
  periodSeconds: 10
```