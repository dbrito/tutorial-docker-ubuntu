<p align="center"><img src="https://cdn.cloudlabs.com.br/wp-content/uploads/2017/07/whale-docker-logo.png"/></p>

# Tutorial Virtualização de Docker no Ubuntu
Nessa tutorial iremos apresentar o que é o Docker e como o mesmo pode ser utilizar para a virtualização no sistema operacional ubuntu.


## *Mas o que é Docker ?

O docker é uma alternativa de virtualização em que o kernel da máquina hospedeira é compartilhado com a máquina virtualizada ou o software em operação, portanto um desenvolvedor pode agregar a seu software a possibilidade de levar as bibliotecas e outras dependências do seu programa junto ao software com menos perda de desempenho do que a virtualização do hardware de um servidor completo. Assim, o docker torna operações em uma infraestrutura como serviços web mais eficientes e flexíveis.

O docker é composto principalmente por dois conceitos:
- Imagem:
- Container:


## 0 - Pré-requisitos
Precisamos apenas de uma máquina Ubuntu com acesso a internet (modo bridge se estiver rodando uma VM), essa máquina Ubuntu também deve ser da arquitetura x86/x64 isso é necessário para que a virtualização do docker ocorra.

## 1 - Instalando o Docker no Ubuntu
1 - Antes de tudo precisamos atualizar o repositório do apt-get
```
$ sudo apt-get update
```
2 - Com o reposotório atualizado podemos instalar os programas necessários para a instalação/execução do Docker
```
$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```
3 - Agora devemos adicionar a chave do repositório do Docker, isso se faz necessário porque temos que adicionar o repositório do docker ao a lista do apt-get, pois o docker não está disponível por padrão.
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
4 - Verificar se a chave foi instalada corretamente
```
$ sudo apt-key fingerprint 0EBFCD88
```
*Caso tenha sido o retorno do comando deve ser semelhando ao trecho abaixo:
```
pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22
```
5- Adicionar o repositório do Docker
```
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
6- **Finalmente** instalar o Docker
```
$ sudo apt-get update
https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
$ sudo apt-get install docker-ce
```

## 2 - Rodando um Container no Docker
Com o docker instalado, você pode rodar containers de uma imagem através do comando
```
$ docker run -d -p 8080:80 nginx
```
A partir disso o docker irá baixar a imagem do nginx e rodara o container da imagem na porta 8080

# 3 - Monitoramento de containers
Para saber se o seu container foi iniciado corretamente você pode usar o comando
```
$ docker ps
```
O mesmo irá listar todos os containers que foram iniciados na máquina
