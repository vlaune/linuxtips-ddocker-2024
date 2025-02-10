FROM ubuntu:18.04
LABEL maintainer="victorh.laune@gmail.com"

# Adicionando o curl para instalar
RUN apt-get update && apt-get install nginx curl -y && rm -rf /var/lib/apt/lists/*

EXPOSE 80

# consigo colocar coisas da internet (baixar) e salvar em algum lugar;
# baixando o prometheus e salvando no /root/node-exporter;
# PS.: Se estiver online, ele não descompacta, para descompactar o arquivo deve estar local.
ADD https://github.com/prometheus/node_exporter/releases/download/v1.6.0/node_exporter-1.6.0.linux-amd64.tar.gz /root/node-exporter

COPY index.html /var/www/html
WORKDIR /var/www/html
ENV APP_VERSION 1.0.0
ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off;"]

# verificar se o container está saudável
# preciso ter um timeout, se não responder em uma quantidade de tempo, ele deve retornar erro
# vai tentar acessar o curl no localhost se falar ele vai finalizar com o exit 1
# o || é OU, executa ou mata.
HEALTHCHECK --timeout=2s CMD curl -f localhost || exit 1

