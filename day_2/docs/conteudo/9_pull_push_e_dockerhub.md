Quando o docker faz um pull de imagem, ele está pegando essa imagem do Registry

Registry são repositórios com imagens de containers, existem vários registrys. Mas o mais popular é DockerHub.
Quando fazemos uma solicitação de imagem, é verificado primeiro na nossa máquina e depois ele vai buscar no DockerHub (por default)

Quando vou fazer o push/upload geralmente vamos enviar para uma cloud /github/gitlab (mas o funcionamento é o mesmo).

Quando vamos fazer um push, devemos
`docker login`
1. passar o username
2. passar o password (que fica em security > new access token > RWD > pega o código e joga na CLI)

Quando subimos uma imagem para o dockerhub, devemos subir com o nome do nosso usuário/imagem. Seria algo assim:
`viclaune/imag-go-lang`

podemos trocar o nome de uma imagem já existente com o `tag`:
`docker image tag go-teste:4.0 linuxtips/go-teste:4.0`

`docker logout` : para encerrar.