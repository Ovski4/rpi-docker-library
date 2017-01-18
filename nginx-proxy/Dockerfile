FROM ovski/rpi-nginx:1.10.2

# Install wget and install/updates certificates
RUN apt-get update \
 && apt-get install -y -q --no-install-recommends \
    ca-certificates \
    wget \
    git \
 && apt-get clean \
 && rm -r /var/lib/apt/lists/*

# Configure Nginx and apply fix for very long server names
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# Install go
ENV GO_VERSION 1.7.4
RUN wget https://storage.googleapis.com/golang/go1.7.4.linux-armv6l.tar.gz
RUN tar -C /usr/local -xzf go${GO_VERSION}.linux-armv6l.tar.gz
ENV GOPATH /root/go
RUN mkdir /root/go
ENV PATH ${PATH}:/usr/local/go/bin

# install forego
RUN go get -u github.com/ddollar/forego
RUN ln -s /root/go/bin/forego /usr/local/bin/forego
RUN chmod u+x /usr/local/bin/forego

ENV DOCKER_GEN_VERSION 0.7.3

RUN wget https://github.com/jwilder/docker-gen/releases/download/${DOCKER_GEN_VERSION}/docker-gen-linux-armhf-${DOCKER_GEN_VERSION}.tar.gz \
 && tar -C /usr/local/bin -xvzf docker-gen-linux-armhf-${DOCKER_GEN_VERSION}.tar.gz \
 && rm docker-gen-linux-armhf-${DOCKER_GEN_VERSION}.tar.gz

COPY ./app /app/
WORKDIR /app/

ENV DOCKER_HOST unix:///tmp/docker.sock

VOLUME ["/etc/nginx/certs"]

ENTRYPOINT ["/app/docker-entrypoint.sh"]
CMD ["forego", "start", "-r"]
