# Pods
***
## O que são e como funcionam?
* Os pods podem ser comparados como containers no "mundo docker"
* O pod é uma "capsula", ou seja, dentro de um pod podem existir 1 ou mais containers.
* A comunicação do kubectl com um pod é feita por uma **Api** podendo essa comunicação ser feita de maneira declarativa ou imperativa.
* Os pods possuem um endereço ip relacionado ao Pod e não ao container, os containers vão ser referenciados pela porta ex: IP:8080.
* Os pods são efêmeros então eles podem deixar de existir a qualquer momento, sendo assim o kubernets tem total liberdade para criar um novo pod, não necessariamente com o mesmo ip, caso um pod deixe de existir.
* Pode acontecer de um container acabar morrendo dentro de um pod e caso ainda tenha um container "saudável" dentro dele ele continuará funcionando, mas caso não exista mais nenhum container funcionando dentro do Pod ele irá ser derrubado e outro será criado dentro dele.
* Os container irão compartilhar o mesmo namespace de rede e IPC, podendo compartilhar volumes.
* E um pod comunicar diretamente com outro Pod