#docker image with ubuntu+voikko as base and default-jre (jre8 at the time of writing..) on top
#basically provides a docker image for java+libvoikko development/apps

FROM ubuntu:16.04
MAINTAINER Teemu Kanstren <tkanstren@gmail.com>

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update && apt-get install -y default-jre libvoikko-dev voikko-fi wget unzip nano
RUN mkdir voikko
WORKDIR voikko
RUN wget http://www.puimula.org/htp/testing/voikko-snapshot-v5/dict-morphoid.zip && unzip dict-morphoid.zip
WORKDIR /

