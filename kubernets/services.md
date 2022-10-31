# Services 
***
## O que é e como Funciona?
***
### O que são?
* Services é um resource do kubernets que permite a comunicação de diferentes aplicações e de diferentes pods.
* Os Services proveem IP's fixo para comunicação.
* Proveem um DNS para um ou mais pods.
* São capazes de fazer balanceamento de cargas
* Os services por mais que associados a pods, caso um pod deixe de existir, o service continuará funcionando.
* É necessário dentro dos pods existir uma lable dentro de metadata que especifique o app, para que assim o service entenda quais pod ele deve atuar.
* Dentro do arquivo .yaml é necessário especificar o type, o kind, o selector, que deve ser qual pod ele atuará de acordo com a label passada e a porta que ele irá ouvir e a porta que ele ira despachar com a tag ```targetPort```.

##### Os services possuem 3 tipos:
* O ClusterIP
* NodePort
* LoadBalancer
***
### ClusterIP
* O service ClusterIP serve para fazer a comunicação entre diferentes pods dentro de um mesmo cluster.
* Comunicação **apenas internamente**, ou seja, dentro do Cluster.
##### Exemplos de pod e svc
![Exemplo Pod](imgs/pod-2.png)
![Exemplo SVC](imgs/svc.png)