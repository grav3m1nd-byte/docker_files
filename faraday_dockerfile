FROM ubuntu:20.04
MAINTAINER Jorge Berrios <jxberrios@gmail.com>

ARG username

ENV TZ="America/New_York"
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN DEBIAN_FRONTEND="noninteractive" apt update && apt install openssh-server sudo wget vim python3-pip dialog apt-utils postgresql -y
#RUN chown postgres /var/lib/postgresql/12/main
RUN wget "https://github.com/infobyte/faraday/releases/download/v3.14.2/faraday-server_amd64.deb" -O /tmp/faraday-server_amd64.deb
RUN apt install /tmp/faraday-server_amd64.deb

RUN useradd -rm -d /home/ubuntu -s /bin/bash -g root -G sudo,faraday -u 1001 $username
RUN echo "$username:test" | chpasswd
RUN service ssh start

EXPOSE 22

VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql", "/home/faraday"]

EXPOSE 5985

RUN sed -e "s/#listen_addresses = 'localhost'/listen_addresses = '*'/g" /etc/postgresql/12/main/postgresql.conf
RUN service postgresql start
RUN pg_ctlcluster 12 main start

CMD ["/usr/sbin/sshd","-D"]

SHELL ["/bin/bash", "-c"]
