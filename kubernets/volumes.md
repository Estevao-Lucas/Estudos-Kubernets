# Volumes
***
## O que são:
***
* Os volumes por sua natureza também são efêmeros e portanto possuem o tempo de vida de um Pod, o ciclo de vida de um volume é independente de um container, mas dependente de um Pod.
* Os volumes são uma maneira de persistir informações dentro de um pod, eles são totalmente dependentes dos pods e caso o Pod que continha o volumes morra, o volume também deixará de existir.
* Porém existem volumes que não dependem da existência de um Pods, eles são chamados de Persistents Volumes
* Um Pod pode ter diferentes tipos de volume simultaneamente.
* Eles são declarados dentro do campo spec do Pod.
***
### HostPath
***
* Esse tipo de volume ao ser declarado no Pod, ele cria um diretório dentro do container, e esse diretório é mapeado para um diretório dentro da máquina que está executando o Pod.
* Esse volume deixa de existir quando o Pod é removido, mas por estar mapeado dentro da máquina os dados não são perdidos.
* Como na versão do Linux é usado uma máquina virtual (minikube), será preciso criar um diretório dentro da máquina virtual para que o diretório seja mapeado para o container.
* Ex sem criação de diretório:
  
![HostPath](imgs/hostpath.png)

```yaml
spec:
  containers:
    - name: <nome do container>
      image:  <image do container>
      volumeMounts:
        - mountPath: /volume-dentro-do-container
          name: volume
  volumes:
    - name: <Nome do Volume>
      hostPath:
        path: /<Caminho>
        type: Directory
```

* Ex com criação de diretório:

![HostPath](imgs/hostpathcreate.png)

```yaml
spec:
  containers:
    - name: <nome do container>
      image:  <image do container>
      volumeMounts:
        - mountPath: /volume-dentro-do-container
          name: volume
  volumes:
    - name: <Nome do Volume>
      hostPath:
        path: /<Caminho>
        type: DirectoryOrCreate 
```