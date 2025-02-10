Dockerfiles existem com o próposito de criar imagens de containers.

Uma imagem é um container parado.
Uma imagem de container utiliza o filesystem em camadas, e nessas camadas é onde passamos as instruções.
Para cada instrução no nosso Dockerfile vamos criar mais uma camada nas nossas imagens.
Uma imagem é completamente Read-Only, quando ela é executada (criar o container) ela tem todas as camadas do read-only e adiciona uma camada read-write no topo.

Vamos criar um ngix a partir de um Ubuntu.

| camada do build        | -> Camada 5 (RW) (Criada quando buildamos o container)
| exec nginx             | -> Camada 4 (RO) (CMD)
| config                 | -> Camada 3 (RO) (COPY)
| update e install nginx | -> Camada 2 (RO) (RUN)
| ubuntu                 | -> Camada 1 - imagem base (uma imagem que ja tem várias camadas) (RO) (FROM)

