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

RUN addgroup -S vagrant && adduser -S vagrant -G vagrant
#RUN ln -sf /usr/share/zoneinfo/Etc/UTC /etc/localtime

RUN apk add --no-cache \
    python3 \
    python3-dev \
  && pip3 install --no-cache-dir --upgrade pip \
  && rm -rf /var/cache/* \
  && rm -rf /root/.cache/*

RUN cd /usr/bin \
  && ln -sf python3 python \
  && ln -sf pip3 pip


FROM amazonlinux:2 as installer
COPY awscli-exe-linux-x86_64.zip .
RUN yum update -y \
  && yum install -y unzip \
  && unzip awscli-exe-linux-x86_64.zip \
  # The --bin-dir is specified so that we can copy the
  # entire bin directory from the installer stage into
  # into /usr/local/bin of the final stage without
  # accidentally copying over any other executables that
  # may be present in /usr/local/bin of the installer stage.
  && ./aws/install --bin-dir /aws-cli-bin/

FROM amazonlinux:2
RUN yum update -y \
  && yum install -y less groff \
  && yum clean all
COPY --from=installer /usr/local/aws-cli/ /usr/local/aws-cli/
COPY --from=installer /aws-cli-bin/ /usr/local/bin/

VOLUME ["/data"]
WORKDIR /data

ENTRYPOINT [ "tail", "-f", "/dev/null" ]

CMD ["/bin/bash"]
