# Introdução a Kubernets
***
## Kubernets
* **Kubernets** é um orquestrador de containers.
* O Kubernets é capaz de gerenciar uma ou mais máquinas em conjunto e trabalhando em paralelo. Esse Grupo de Máquinas trabalhando em conjunto e dividindo o seu poder computacional é chamado de **Cluster**.
* O gerenciamento realizado pelo kubernets é feito de maneira similar ao docker, em que ele vai escolher uma determinada maquina virtual para executar um container e caso surja outro container, ele é capaz de criar uma nova VM ou alocar ele na mesma VM em que outro container está sendo executado, bem como caso as VMs cheguem em seu limite computacional, ele irá cirar uma outra VM.
***
## Resources 
* **Resources**, o Kubernets possue dentro de sua aquitetura os **resources** que auxiliam no desenvolvimento e apresentam algumas soluções prontas, exemplos de resources são os *pods*, *deploy*, *job*, *rs* e outros.
* Dentro dos **Clusters** existem os os **Masters** que são responsáveis por:
* Manter e atualizar o estado desejado, receber e executar novos comando e gerenciar os *Nodes*.
* Os **Nodes** executam os pods que executam os containers.