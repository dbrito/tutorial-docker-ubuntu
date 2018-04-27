

<p align="center"><img src="https://cdn.cloudlabs.com.br/wp-content/uploads/2017/07/whale-docker-logo.png"/></p>

# Tutorial Virtualização de Docker no Ubuntu
Nessa tutorial iremos apresentar o que é o Docker e como o mesmo pode ser utilizado para a virtualização em máquinas Ubuntu.


## *Mas o que é Docker ?

O Docker é uma plataforma de virtualização criada com o objetivo de otimizar a criação, o teste e implantação de aplicações, só que diferente das virtualizações convencionais o Docker não utiliza o kernel inteiro do sistema operacional da máquina virtual ao invés disso utiliza o kernel da própria máquina hospedeira, gerando menos gasto de memoria e principalmente vacilitando o processo de desenvolvimento já que o Docker vai funcionar da mesma forma independente do sistema operacional.

### Principais Componentes:
- Imagem: Seria o template do container é nela que difinimos o sistema operacional, quais programas serão utilizados, e quais aplicações devem ser executadas.
- Container: Seria uma instancia da imagem sendo executada.

\* Fazendo uma analogia com orientação a objeto, a Imagem seria equivalente a uma Classe, e um Container seria equivalente a uma instância dessa classe.

### VMs x Containers
<p align="center"><img src="https://cloudlightning.eu/wp-content/uploads/2017/01/virtual-containers.jpg"/></p>

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
Caso você queira saber mais detalhes sobre o container (portas utilizada, tipo de rede, etc) basta executar o comando
```
docker inspect [ID DO CONTAINER]
```

Caso você queira encerrar algum container basta executar o comando
```
docker rm [ID DO CONTAINER]
```
*O ID do container pode ser encontrado no comando ``docker ps``.

## 4 - Acessando os containers
Com os containers "de pé" para acessá-los basta bater no IP da máquina Ubuntu passando a porta exposta durante o processo de subir o container.
**Ex:** Se você rodou o container na porta 8080 (``$ docker run -d -p 8080:80 nginx``) basta acessar o IP na porta 8080 ``172.6.1.66:8080``

## 5 - Executando comando em containers
Para executar comando no container basta executar o comando abaixo
``
docker exec -it c32a365997a1 ls -la
``

**Traduzindo:**  ``docker exec -it [ID DO CONTAINER] [COMANDO A SER EXECUTADO]``




## *Links úteis:
https://docs.docker.com/install/linux/docker-ce/
https://www.mundodocker.com.br/
https://www.digitalocean.com/community/tutorials/como-instalar-e-utilizar-o-docker-primeiros-passos-pt
https://stackoverflow.com/questions/28089344/docker-what-is-it-and-what-is-the-purpose?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa
