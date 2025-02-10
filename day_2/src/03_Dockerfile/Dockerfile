FROM ubuntu:18.04

# (rotulo) passar informações úteis, como maintainer por exemplo
LABEL maintainer="victorh.laune@gmail.com"

RUN apt-get update && apt-get install nginx -y && rm -rf /var/lib/apt/lists/*
EXPOSE 80
COPY index.html /var/www/html
WORKDIR /var/www/html
ENV APP_VERSION 1.0.0

# O docker entende que esse é o principal processo, se ele morrer o container morre tbm.
# Será executado quando o container estiver de pé
ENTRYPOINT ["nginx"]

# o CMD sempre vai ser parametro do ENTRYPOINT, repare que o "nginx" saiu daqui!
CMD ["-g", "daemon off;"]

