# Tutorial Virtualização de Docker no Ubuntu

Nessa tutorial iremos apresentar o que é o Docker e como o mesmo pode ser utilizar para a virtualização no sistema operacional ubuntu.


## *Mas o que é Docker ?

O docker é uma alternativa de virtualização em que o kernel da máquina hospedeira é compartilhado com a máquina virtualizada ou o software em operação, portanto um desenvolvedor pode agregar a seu software a possibilidade de levar as bibliotecas e outras dependências do seu programa junto ao software com menos perda de desempenho do que a virtualização do hardware de um servidor completo. Assim, o docker torna operações em uma infraestrutura como serviços web mais eficientes e flexíveis.

O docker é composto principalmente por dois conceitos:
- Imagem:
- Container:


## *Em que ele pode ser usado ?
The file explorer is accessible using the button in left corner of the navigation bar. You can create a new file by clicking the **New file** button in the file explorer. You can also create folders by clicking the **New folder** button.

## 0 - Pré-requisitos

All your files are listed in the file explorer. You can switch from one to another by clicking a file in the list.

## 1 - Instalando o Docker no Ubuntu
1 - Atualizar o repositório do apt-get
```
$ sudo apt-get update
```
2 - Instalar os programas necessários para a instalação do Docker
```
$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```
3 - Adicionar a chave do repositório do Docker
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
