# Horizontal Pod Autoscaler
***
## O que é?
***
* O Horizontal Pod Autoscaler (HPA) é um recurso do Kubernetes que permite que você aumente ou diminua o número de pods em um deployment baseado em métricas de CPU ou memória.
* O HPA irá realizar o escalonamento baseado em métricas de CPU ou memória, mas também pode ser configurado para basear o escalonamento em métricas personalizadas, tudo isso de maneira automática.
* Para utilizar o HPA é necessária que seja declarado quanto de CPU e memória o pod pode utilizar dentro do campo resources.
* O HPA utiliza um Metrics Server para atuar em conjunto e assim ter informações sobre as métricas de CPU e memória. 
* No caso do Linux é possível utilizar o Metrics Server a partir do minikube com o comando `minikube addons enable metrics-server`. Ele é uma extensão do minikube que permite que o HPA funcione corretamente.
* Ex de definição dos recursos no pod que pode estar dentro de um deployment:
```yaml
resources:
  requests:
    memory: "64Mi"
    cpu: "250m"
```
* Ex de definição do HPA:
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: hpa-example
spec:
    scaleTargetRef:
        apiVersion: apps/v1
        kind: Deployment
        name: deployment-example
    minReplicas: 1
    maxReplicas: 10
    metrics:
    - type: Resource
        resource:
        name: cpu
        target:
            type: Utilization
            averageUtilization: 50 #50% de utilização da CPU, realizando o escalonamento quando atingir 50% de utilização
```
#### Breve resumo Vertical Pod Autoscaler
***
* O VerticalPodAutoscaler remove a necessidade de definir limites e pedidos por recursos do sistema, como cpu e memória. Quando definido, ele define os consumos de maneira automática baseada na utilização em cada um dos nós, além disso, quanto tem disponível ainda de recurso.
* Mais informações no link: <https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler>