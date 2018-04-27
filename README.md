<p align="center"><img src="https://cdn.cloudlabs.com.br/wp-content/uploads/2017/07/whale-docker-logo.png"/></p>

# Tutorial Virtualização de Docker no Ubuntu
Nessa tutorial iremos apresentar o que é o Docker e como o mesmo pode ser utilizar para a virtualização no sistema operacional ubuntu.


## *Mas o que é Docker ?

O docker é uma alternativa de virtualização em que o kernel da máquina hospedeira é compartilhado com a máquina virtualizada ou o software em operação, portanto um desenvolvedor pode agregar a seu software a possibilidade de levar as bibliotecas e outras dependências do seu programa junto ao software com menos perda de desempenho do que a virtualização do hardware de um servidor completo. Assim, o docker torna operações em uma infraestrutura como serviços web mais eficientes e flexíveis.

O docker é composto principalmente por dois conceitos:
- Imagem:
- Container:

### VMs x Containers
<p align="center"><img src="http://blog.ti.lemaf.ufla.br/content/images/2016/05/mp234.png"/></p>

## 0 - Pré-requisitos
Precisamos apenas de uma máquina Ubuntu com acesso a internet (modo bridge se estiver rodando uma VM), essa máquina Ubuntu também deve ser da arquitetura x86/x64 isso é necessário para que a virtualização do docker ocorra.
*Para saber a arquitetura da sua máquina ubuntu basta rodar o comando ```uname -a```

## 1 - Instalando o Docker no Ubuntu
Antes de tudo precisamos atualizar o repositório do apt-get
```
$ sudo apt-get update
```
Com o repositório atualizado podemos instalar os programas necessários para a instalação/execução do Docker
```
$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```
Agora devemos adicionar a chave do repositório do Docker, isso se faz necessário porque temos que adicionar o repositório do docker ao a lista do apt-get, pois o docker não está disponível por padrão.
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
Se pode verificar se a chave foi instalada corretamente com o comando
```
$ sudo apt-key fingerprint 0EBFCD88
```
*Caso tenha sido, o retorno do comando deve ser semelhando ao trecho abaixo:
```
pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22
```
Com a chave adicionada agora adiconamos o repositório do Docker
```
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
Com o repositório adicionado, **finalmente 🙌🙌** podemos instalar o Docker
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
A partir disso o docker irá rodar um container (``run``) em background (``-d``), esse container estará exposto na porta 8080(``-p 8080:80``) e irá baixar a imagem do ``nginx``.

## 3 - Monitorando os containers
Depois de "rodar" um container você precisar saber se o mesmo foi iniciado corretamente e se ele ainda está de pé isso pode ser alcançado através do comando
```
$ docker ps
```
O mesmo irá listar todos os containers que foram iniciados na máquina
```$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
2ca40d5e3b8f        nginx               "nginx -g 'daemon ..."   9 minutes ago       Up 8 minutes        80/tcp              xenodochial_pike
```
Caso você queira encerrar algum container basta executar o comando
```
docker rm 2ca40d5e3b8f
```
*Onde o ``2ca40d5e3b8f`` seria o ID do container (que é encontrado no comando ``docker ps``).

## 4 - Acessando os containers
Com os containers "de pé" para acessá-los basta bater no IP da máquina Ubuntu passando a porta exposta durante o processo de subir o container.
**Ex:** Se você rodou o container na porta 8080 (``$ docker run -d -p 8080:80 nginx``) basta acessar o IP na porta 8080 ``172.6.1.66:8080``

Fontes utilizadas:
https://docs.docker.com/install/linux/docker-ce/
https://www.mundodocker.com.br/
