FROM nginx:1.11

# Set timezone
RUN echo "Europe/Berlin" > /etc/timezone \
 && dpkg-reconfigure -f noninteractive tzdata


ADD nginx.conf /etc/nginx/
RUN rm -f /etc/nginx/conf.d/*
#Add Backend vhost conf
ADD admin.sulu.dev.conf /etc/nginx/conf.d/
# add Frontend vhost conf
ADD sulu.dev.conf /etc/nginx/conf.d/

ENV CERTIFICATE_DIR=/usr/local/app/certs

RUN mkdir -p $CERTIFICATE_DIR
RUN openssl req -new -x509 -nodes \
-subj "/CN=sulu.dev/O=Sulu CMS/C=DE/ST=Heilbronn/L=Neckarsulm" -keyout \
$CERTIFICATE_DIR/server.key -out $CERTIFICATE_DIR/server.crt

RUN echo "upstream php-upstream { server php-fpm:9000; }" > /etc/nginx/conf.d/upstream.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]
