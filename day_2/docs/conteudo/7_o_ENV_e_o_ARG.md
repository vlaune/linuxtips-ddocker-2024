- O `ENV` serve para criar uma variável de ambiente dentro do container.
- o `ARG` serve para criar uma variável de ambiente na imagem, no momento de build.

Para verificar se as variáveis estão no container, podemos passar um `inspect`.
Poderia trocar o arg na buildagem:
`docker build -t go-teste:4.0 --build-arg VERSION=2.00`