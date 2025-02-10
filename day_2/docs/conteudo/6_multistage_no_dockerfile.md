Multistage é uma forma de fazer com que as imagens fiquem mais performática e menores;

Montando uma imagem de container, quando subirmos a réplica de container, se a imagem tiver 500mb, o container terá 500mb + info geradas com a execução do container.
- Pense sempre como otimizar a imagem e torná-la menor.
- Ex.: imagens com distro linux bem enxutas (Alpine Linux por exemplo).
    - Tem versão Alpine pode ser utilizada para várias aplicações, (Python, Redis...)

Ter imagem pequena é muito bom para quando formos fazer pull, e diminuir banda.


Vamos ao 05_Dockerfile
E tivemos uma imagem de quase 1GB com o nosso programinha simples.

```Dockerfile
# Estou dando um "nome" para toda essa parte
FROM golang:1.18 as buildando
WORKDIR /app
COPY . ./
RUN go mod init hello
RUN go build -o /app/hello
# aqui acaba o build


# escolho uma outra imagem que pode rodar a aplicacao criada
FROM alpine:3.15.9

# copiando do buildando o binário gerado no app/hello 
COPY --from=buildado /app/hello /app/hello

# aqui é a execução de toda a primeira parte
CMD ["/app/hello"]
```

Temos agora uma imagem fazendo a mesma coisa com 7.35 MB


Ebook Multistage
- O multi-stage traz a possibilidade de criar uma espécie de pipeline no dockerfile, inclusive podendo utilizar duas entradas FROM.
- É utilizado quando queremos compilar a nossa aplicação em um container e executá-la, porém não queremos ter a enorme quantidade de pacotes instalados.
- Com o segundo código, divididos nosso Dockerfile em duas seções, cada entrada FROM define o início de um bloco.
- Nosso primeiro bloco:
```dockerfile
FROM golang AS buildando 
# -- Estamos utilizando a imagem do Golang para criação da imagem de container, e aqui estamos apelidando esse bloco como "buildando".

ADD . ./ 
# -- Adicionando o código de nossa app dentro do container.

WORKDIR /app 
# -- Definindo que o diretório de trabalho é o "/app", ou seja, quando o container iniciar, estaremos nesse diretório.

RUN go build -o /app/hello 
# -- Vamos executar o build de nossa app Golang.
```
- Nosso segundo bloco:
```dockerfile
FROM alpine:3.15.9  
# -- Iniciando o segundo bloco e utilizando a imagem do Alpine para criação da imagem de container.

COPY --from=buildando /app/hello /app/hello
# -- Aqui está a mágica: vamos copiar do bloco chamado "buildando" um arquivo dentro de "/app/hello" para o diretório "/app" do container que estamos tratando nesse bloco, ou seja, copiamos o binário que foi compilado no bloco anterior e o trouxemos para esse.

CMD ["/app/hello"] 
# -- Aqui vamos executar a nossa sensacional app. :)
```

Na segunda etapa, utilizamos a imagem do Golang e todos os seus pacotes para buildar a nossa aap, porém descartamos a primeira imagem e somente copiamos o binário para o segundo bloco, onde estamos utilizando a imagem do Alpine, que é superenxuta.