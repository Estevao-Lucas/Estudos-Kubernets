# :penguin: Instalação no Linux
***
## :canoe: Instalação Kubectl
***
* Acesse o link para instalação do [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) e siga o passo a passo.
* Cole esse comando no terminal para instalação dos binarios ```curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"```
* Validação do binario (Opcional) ```curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"```
* Caso esse comando ```echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check``` imprima **OK** ou **SUCESSO** a instalação funcionou.
* Instalação do Kubectl ```sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl```
* Verificar se instalou certo ```kubectl version --client```
***
## :boat: Instalação MiniKube
### :desktop_computer: Clusters
***
* Para instalação do MiniKube use os comando ```curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64```
```sudo install minikube-linux-amd64 /usr/local/bin/minikube```
* Para verificar se a instalação ocorreu de maneira correta utilize o comando ```minikube version```
* Para iniciar um cluster utilize ```minikube start --vm-driver=<Driver de virtualização>``` um exemplo de driver de virtualização caso você ja tenha instalado o VirtualBox é o ```virtualbox``` Então o comando ficaria ```minikube start --vm-driver=virtualbox```
* Verificar os nodes ```kubectl get nodes```
***
* Passo a Passo mais detalhado
![Passo a Passo](passos.png)
## :cloud: Inicialização no GCP (Bônus)
### :dollar: Podem ser cobrados pelo uso
* Crie um projeto dentro do Google Cloud Plataform e escolha um recurso no caso **Kubernets Engine**.
* Após a ativação da engine podemos pedir para criar um cluster e escolhendo algumas opçoes como Zona e Versão do GCP.
* Após isso basta acessar o cluster clicando em Conectar, o GCP vai gerar um terminal Linux que já vem configurado.




