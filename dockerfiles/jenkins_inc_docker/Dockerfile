FROM jenkins/jenkins:lts

USER root
# RUN git config --global http.sslverify false
RUN touch /etc/apt/apt.conf.d/99verify-peer.conf \
&& echo >>/etc/apt/apt.conf.d/99verify-peer.conf "Acquire { https::Verify-Peer false }"
RUN apt-get update
RUN apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
 RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -   
 RUN apt-key fingerprint 0EBFCD88
 RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
 RUN apt-get update && apt-get install -y  docker-ce docker-ce-cli containerd.io  


RUN usermod -a -G docker jenkins

USER jenkins