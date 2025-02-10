







# Descomplicando Namespaces
- O Namespace é a forma de fazer o isolamento de filesystem, usuários, processos, redes, etc.
- Vamos utilizar o Namespace do Linux para montar algo similar à um container.
- Para isso, vamos utilizar o debootstrap
    - Ferramenta do debian para trazer toda a estrutura de uma distrobuição debian e colocar em um diretório.
    - Colocar o debian inteiro dentro de um diretório.
        - Vamos estar dentro do diretório Debian e achar que aquele é o mundo. Similar ao que faz o chroot.
        - O resultado é como copiar todo o "/" do debian e levar para um pasta.

- Para mexer com Namespace temos um cara chamado `unshare`;
- É o comando com que tenhamos o `Namespace`. Vamos dar uma olhada no help do `unshare`:
[unshare](/estudos/LinuxTips/Descomplicando_Docker_2024/Day1_Fundamentos_do_Docker_e_Primeiros_Passos/docs/1_unshare_help.png)
[Falta terminar isso aqui!]

# Descomplicando Cgroups
[Falta terminar isso aqui!]

# Copy-On-Write e como ele funciona
[Falta terminar isso aqui!]

# Criando e gerenciando os primeiros containers
```sh
docker container run --name awesome_nightingale -it ubuntu:latest
// i == iterativide
// t == terminal 
// :latest == versão, em PRD sempre passe a versão que deseja.
// name == para definir o nome do container
```
**Sem matar o terminal**:
![img_container_ls](/estudos/LinuxTips/Descomplicando_Docker_2024/Day1_Fundamentos_do_Docker_e_Primeiros_Passos/docs/img_container_ls.png)
- Teremos o `/bin/bash` ainda execução, se matarmos o terminal que está executando-o, o container também morrerá, por que ele "não precisa mais estar de pé";

```sh
docker container attach 3716e3cad9fc
// para conectar com um container em execução

// > matamos o container com o terminal

# >> Mudando estado do container <<
docker container start awesome_nightingale
// restartar o container
docker container stop awesome_nightingale
// stopa o container
docker container pause awesome_nightingale
// pausa o container
docker container unpause awesome_nightingale
// despausa o container

# removendo o container
docker container rm aweseoma_nightingale
// removido até dos já executados

docker container prune
// vai remover todos os containers que estao parados
``` 
- Não podemos dar o mesmo nome de um container que já foi executado, irá gerar um erro.


# Visualizando métricas e a utilização de recursos pelo containers
Tenho os containers, mas quero pegar mais informações e detalhes sobre a execução deles.
```sh
docker container stats
// vai mostrar um painel em streaming mostrando como está rodando
docker container stats --no-stream
// vai fazer um snapshot do momento 
```

Mas se eu quiser ver o que está rodando e como está rodando dentro do container?
```sh
docker container top toskao1
```

Outro ponto importante é ver os logs
```sh
docker container logs --details toskao1
// apresenta todos os detalhes de log do container

docker container logs toskao1
// apresenta os logs do container

docker container logs -f toskao1
// trava o terminal e fica esperando aparecer os logs
```


# Visualizando e inspecionando imagens e containers
```sh
docker container ls 
docker container ls -a

docker container rm toskao2
// se estiver em execucao ele n remove, mas podemos passar a flag -f (force) para excluir mesmo rodando

docker image ls
// para visualizar as imagens que estão local
docker image rm ID_da_imagem
// remover a imagem local, se estiver sendo utilizada por um container, ela não vai ser excluída.


docker inspect toskao
// traz informações sobre o container, quando criado, ponto de montagem, imagens, redes...
docker container inspect toskao
// informacao sobre o container
docker image inspect ID_da_IMAGE
// informacao sobre a image
```



# Criando um container Dettached e o Docker exec
Como utilizar o `-d` (Dettached) e o `exec`
```sh
docker container run -d --name meu-nginx nginx:latest
```
com o -d ele faz com que o container fique rodando em segundo plano, ou modo deamon.
[] print do docker container ls com o COMMAND.

Temos aqui o /docker-entrypoint. é um script em que mantém o nginx em execução. na porta 80/tcp.

Se eu tentar fazer um attach nesse docker, eu vou "entrar" no processo existente do container do nginx.

```sh
docker container exec -it meu-nginx bash
```
com o `exec -it` eu consigo executar comandos dentro do container. 
com o comando acima eu consigo rodar o bash dentro do container.

```sh
docker container run -d -p 8080:80 --name meu-nginx nginx
```
Com o `-p` eu defino a porta local que eu quero expor o container.
- No exemplo do ls vimos que ele apresenta a porta 80, mas é a 80 do container que está "fechada",
com o comando -p eu defino que quero q seja exposta na porta 8080 do host o que deve chegar da porta 80 do container.

```sh
docker pull centos:7
```
- faço o download da imagem do centos:7 e deixo salvo na minha máquina local.

```sh
docker container create --name opa nginx
```
- ele não fica rodando, mas está criado, esperando ser executado.



# Desafio prático do Day 1
- Colocar o Docker para rodar em uma VM!
