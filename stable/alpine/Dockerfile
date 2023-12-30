FROM python:3.7-alpine

LABEL maintainer="autor"
ENV PYTHONUNBUFFERED=1 \ 
    ADDRESS=0.0.0.0 \
    PORT=9999 \
    SSLADDRESS=0.0.0.0 \
    SSLPORT=9998

RUN apk --update add --no-cache --virtual .build-deps \
    build-base \
    python3-dev \
    linux-headers \
    openssl-dev \
    libffi-dev \
  && pip3 install --no-cache-dir webssh \
  && apk del .build-deps \
  && rm -rf /var/cache/apk/* /tmp/* /var/tmp/*

ADD public_key.crt root/
ADD private_key.pem root/

EXPOSE $PORT
EXPOSE $SSLPORT

ENTRYPOINT wssh --fbidhttp=False --address=$ADDRESS --port=$PORT --ssladdress=$SSLADDRESS --sslport=$SSLPORT --certfile='/root/public_key.crt' --keyfile='/root/private_key.pem'
