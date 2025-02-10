FROM golang:1.18 as buildando
WORKDIR /app
COPY . ./
RUN go mod init hello
RUN go build -o /app/hello

FROM alpine:3.15.9
COPY --from=buildando /app/hello /app/hello

# Adicionando variáveis de ambiente
ENV APP="hello_world"

ARG VERSION="1.0.0"
RUN echo "Essa imagem esta na versao: $VERSION"

CMD ["/app/hello"]