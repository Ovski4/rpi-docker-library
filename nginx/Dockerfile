FROM resin/rpi-raspbian:jessie-20161207

ENV NGINX_VERSION 1.10.2

RUN apt-get update
RUN apt-get install -y wget make gcc libpcre3 libpcre3-dev zlib1g-dev libbz2-dev libssl-dev

RUN wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz
RUN tar zxvf nginx-${NGINX_VERSION}.tar.gz

WORKDIR ./nginx-${NGINX_VERSION}

RUN ./configure \
    --sbin-path=/usr/sbin/nginx \
    --conf-path=/etc/nginx/nginx.conf \
    --error-log-path=/var/log/nginx/error.log \
    --pid-path=/var/run/nginx.pid \
    --http-log-path=/var/log/nginx/access.log \
    --http-client-body-temp-path=/var/lib/nginx/body \
    --http-proxy-temp-path=/var/lib/nginx/proxy \
    --with-http_stub_status_module \
    --http-fastcgi-temp-path=/var/lib/nginx/fastcgi \
    --with-debug \
    --with-http_gzip_static_module \
    --with-http_v2_module \
    --with-http_ssl_module \
    --with-pcre-jit

RUN make

RUN mkdir -p /var/lib/nginx/body
RUN mkdir -p /var/lib/nginx/fastcgi

RUN make install

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

COPY nginx.conf /etc/nginx/nginx.conf
RUN mkdir /etc/nginx/conf.d

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]

