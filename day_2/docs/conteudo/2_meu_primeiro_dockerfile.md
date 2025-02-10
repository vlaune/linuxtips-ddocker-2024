O Dockerfile é um arquivo de texto que passamos instruções para buildar uma imagem de container.
São poucas instruções, e todas em maiúsculo.
O nome do arquivo deve ser `Dockerfile`.

```docker
# Da onde vem e quem eu vou me basear para criar a imagem
FROM ubuntu:18.04

# Quando preciso executar algum comando quando a imagem do container está sendo buildada
# Cada RUN vai ser uma camada, então faça todo o RUN na mesma camada
# O build não tem como perguntar nada, então faça o -y para dar yes em tudo.
RUN apt-get update && apt-get install nginx -y

# A porta do container que vai estar aberta para conectarem
EXPOSE 80

# Executa um comando, diferente do RUN ele executa no tempo de criação do container.
# O container quando estiver pronto, ele executa esse comando.
# Comandos sao passados em formato de lista
CMD ["nginx", "-g", "daemon off;"]
```

Quando criado o Dockerfile vamos fazer que o build da imagem:
`docker image build -t meu-nginx:1.0 .`
`-t` = tag, nome e versão
`.` = local onde está o arquivo Dockerfile

Vamos agora buildar o container:
`docker container run -d -p 8080:80 --name meu-nginx meu-nginx:1.0`

- Não é interessante fazer a instalação do nginx no ubuntu, vai ficar muito pesado.