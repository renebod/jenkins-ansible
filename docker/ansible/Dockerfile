#FROM alpine:latest
FROM alpine:3.7
MAINTAINER Hive Solutions

EXPOSE 22

RUN apk add --update \
    openssh \
    openjdk8 \
    git \
    python \
    python-dev \
    py-pip \
    sshpass \
    ansible=2.4.1.0-r0
RUN ssh-keygen -A
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
RUN adduser -D jenkins && (echo "jenkins:jenkins" | chpasswd) && (echo "root:root" | chpasswd)

COPY requirements.txt /tmp/
RUN pip install --requirement /tmp/requirements.txt
COPY . /tmp/

RUN mkdir /home/jenkins/.ssh
COPY known_hosts /home/jenkins/.ssh
RUN chown -R jenkins:jenkins /home/jenkins

CMD ["/usr/sbin/sshd", "-D"]
