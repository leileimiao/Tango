# Autolab - autograding docker image

FROM ubuntu:18.04
MAINTAINER Honglei Zhang <zhanghonglei1997@gmail.com>
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
&& sed -i s@/archive.ubuntu.com/@/mirror.tuna.tsinghua.edu.cn/@g /etc/apt/sources.list \
&& sed -i s@/security.ubuntu.com/@/mirror.tuna.tsinghua.edu.cn/@g /etc/apt/sources.list
ARG http_proxy="http://162.105.89.151:3128/" 
ARG https_proxy="http://162.105.89.151:3128/"
RUN apt-get update && apt-get install -y \
	gcc-multilib \
    perlbrew \
    make \
    gcc-4.8\
    gcc-4.8-multilib\
    build-essential \
    python2.7 \
    valgrind 3.2.1 \
    bsdmainutils \
    diffutils \
    curl \
    tcl8.5 \
    tcl8.5-dev \
    tk8.5-dev \
    tk8.5 \
    bison \
    flex \
    git \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* \
&& dpkg-reconfigure -f noninteractive tzdata 
# Install autodriver
WORKDIR /home
RUN useradd autolab
RUN useradd autograde
RUN mkdir autolab autograde output mount
RUN chown autolab:autolab autolab
RUN chown autolab:autolab output
RUN chown autograde:autograde autograde

RUN git clone https://github.com/leileimiao/Tango.git
WORKDIR Tango/autodriver
RUN make clean && make
RUN cp autodriver /usr/bin/autodriver
RUN chmod +s /usr/bin/autodriver

# Clean up
WORKDIR /home
RUN apt-get remove -y git
#RUN rm tango.tar
RUN apt-get -y autoremove
RUN rm -rf Tango/

# Check installation
RUN ls -l /home
RUN which autodriver

