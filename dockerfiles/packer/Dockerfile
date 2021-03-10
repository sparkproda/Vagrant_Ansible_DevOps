FROM alpine:3.7

# Set environment variable for downloading vault version.
ENV PACKER_VERSION=1.7.0

RUN apk update \
    && apk add --update \
       ca-certificates \
       unzip \
       wget \
	   bash \
    && rm -rf /var/cache/apk/* \ 
    && wget -P /tmp/ https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip \
    && mkdir -p /opt/packer \
    && unzip /tmp/packer_${PACKER_VERSION}_linux_amd64.zip  \
	  && mv packer /usr/local/bin/packer \
    && mkdir -p /data

RUN apk add --update --no-cache docker openrc \
    && apk add --no-cache ansible \
    && rm -rf /tmp/*  \
    && rm -rf /var/cache/apk/*  
RUN rc-update add docker boot    

RUN adduser -S jenkins -G docker


RUN apk add --no-cache \
    python3 \
    python3-dev

RUN cd /usr/bin \
  && ln -sf python3 python \
  && ln -sf pip3 pip

VOLUME ["/data"]
WORKDIR /data

ENTRYPOINT [ "tail", "-f", "/dev/null" ]

CMD ["/bin/bash"]
