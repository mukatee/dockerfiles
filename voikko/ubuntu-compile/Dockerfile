#voikko finnish spelling library docker build script
#just the basic development library and finnish dictionary included
#this script downloads the voikko sources and dependencies, compiles them, and downloads the morphoid dictionary files
#it removes the compilation dependencies (g++ etc) to keep the image smaller. this is all done in one step (to avoid creating extra docker layers)
#there is another script that just install directly the libvoikko-dev using apt-get. for ubuntu that is likely the easier solution
#this script is mainly here as reference for anyone who might want to compile it for themselves or to find some references for another base distro where
#libvoikko-dev might not be available

FROM ubuntu:16.04
MAINTAINER Teemu Kanstren <tkanstren@gmail.com>

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN mkdir voikko
WORKDIR voikko

RUN buildDeps='wget g++ python3 pkg-config foma-bin' && \
    apt-get update && apt-get install -y $buildDeps && \
    wget http://www.puimula.org/voikko-sources/libvoikko/libvoikko-4.0.2.tar.gz && \
      tar -xzf libvoikko-4.0.2.tar.gz && \
      rm libvoikko-4.0.2.tar.gz && \
    wget http://www.puimula.org/voikko-sources/voikko-fi/voikko-fi-2.0.tar.gz && \
      tar -xzf voikko-fi-2.0.tar.gz && \
      rm voikko-fi-2.0.tar.gz && \
    cd libvoikko-4.0.2 && \
      ./configure --prefix=/usr/local/voikko --with-dictionary-path=/usr/local/voikkodict --disable-hfst && \
      make && make install && \
      rm -rf * && \
    cd ../voikko-fi-2.0 && \
      PATH=/usr/local/voikko/bin:$PATH make vvfst && \
      make vvfst-install DESTDIR=/usr/local/voikkodict && \
      rm -rf * && \
    apt-get purge -y --auto-remove $buildDeps
RUN wget http://www.puimula.org/htp/testing/voikko-snapshot-v5/dict-morphoid.zip && unzip dict-morphoid.zip
WORKDIR /
