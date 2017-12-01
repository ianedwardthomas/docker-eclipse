#FROM ubuntu:16.04
FROM phusion/baseimage:0.9.22

MAINTAINER Ian Thomas <ianedwardthomas@gmail.com>


# Install the basic
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get install -y build-essential software-properties-common \
    byobu curl git htop man unzip vim wget libwebkitgtk-3.0-0 \
    xfonts-base lxde tightvncserver lxterminal python-all-dev \
    python-numpy  libproj-dev sqlite3 libsqlite3-dev && \
  rm -rf /var/lib/apt/lists/*

# Install Java 8
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle


# Setup user
RUN adduser --home /home/ubuntu --disabled-password --gecos '' ubuntu
RUN echo "ubuntu ALL=NOPASSWD: ALL" >> /etc/sudoers


# enable SSH
RUN rm -f /etc/service/sshd/down

RUN mkdir /etc/service/vnc
COPY vncstart /etc/service/vnc/run
RUN chmod u+x /etc/service/vnc/run

COPY run.sh /run.sh
RUN chmod 755 /run.sh

ARG ECLIPSEBUNDLE=eclipse-inst-linux64

ARG BUNDLELOC=https://www.eclipse.org/downloads/download.php?file=/oomph/epp/oxygen/R/$ECLIPSEBUNDLE.tar.gz&r=1


# Regenerate SSH host keys. baseimage-docker does not contain any, so you
# have to do that yourself. You may also comment out this instruction; the
# init system will auto-generate one during boot.
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

USER ubuntu
WORKDIR /home/ubuntu

# Install R Packages


# Install KNIME
RUN wget $BUNDLELOC -O /home/ubuntu/$ECLIPSEBUNDLE.tar.gz -q
RUN ls /home/ubuntu
RUN tar vxzf $ECLIPSEBUNDLE.tar.gz
RUN chmod +x /home/ubuntu/eclipse-installer/eclipse-inst

#RUN mkdir /home/ubuntu/Desktop
#RUN ln -s /home/ubuntu/eclipse/eclipse /home/ubuntu/Desktop/eclipse
#RUN touch .Xresources

EXPOSE 5901
EXPOSE 22

USER root

CMD ["/sbin/my_init"]
