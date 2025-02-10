FROM golang:1.18
WORKDIR /app

# Quero copiar tudo que está no mesmo nível do diretório
# e carregue tudo para o /app
COPY . ./

RUN go mod init hello
RUN go build -o /app/hello

CMD ["/app/hello"]

