FROM ubuntu:20.04
MAINTAINER Jorge Berrios <jxberrios@gmail.com>

ARG username

VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql", "/home/faraday"]

ENV TZ="America/New_York"
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN DEBIAN_FRONTEND="noninteractive" apt update && apt install openssh-server sudo wget vim python3-pip dialog apt-utils -y
RUN wget "https://github.com/infobyte/faraday/releases/download/v3.14.2/faraday-server_amd64.deb" -O /tmp/faraday-server_amd64.deb

RUN useradd -rm -d /home/ubuntu -s /bin/bash -g root -G sudo -u 1001 $username
RUN echo "$username:test" | chpasswd
RUN service ssh start

EXPOSE 22

EXPOSE 5985

CMD ["/usr/sbin/sshd","-D"]

SHELL ["/bin/bash", "-c"]
