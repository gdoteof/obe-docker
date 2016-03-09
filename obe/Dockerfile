FROM phusion/baseimage

MAINTAINER Geoff Golder

RUN apt-get update && apt-get install -y git

RUN apt-get install -y wget build-essential

RUN wget http://www.tortall.net/projects/yasm/releases/yasm-1.2.0.tar.gz && \
    tar xfzv yasm-1.2.0.tar.gz && \
    cd yasm-1.2.0/ && ./configure --prefix=/usr && make -j5 && sudo make install && cd ..

RUN apt-get install -y libtwolame-dev autoconf libtool

RUN git clone https://github.com/ob-encoder/fdk-aac.git && \
    cd fdk-aac && autoreconf -i && ./configure --prefix=/usr --enable-shared && \
    make -j5 && sudo make install && cd ..

RUN git clone https://github.com/ob-encoder/libav-obe.git && \
    cd libav-obe && ./configure --prefix=/usr --enable-gpl --enable-nonfree --enable-libfdk-aac --disable-swscale-alpha --disable-avdevice && \
    make -j5 && sudo make install && cd ..

RUN git clone https://github.com/ob-encoder/x264-obe.git && \
    cd x264-obe/ && ./configure --prefix=/usr --disable-lavf --disable-swscale --disable-opencl && \
    make -j5 && sudo make install-lib-static && cd ..

RUN git clone https://github.com/ob-encoder/libmpegts-obe.git && \
    cd libmpegts-obe/ && ./configure --prefix=/usr && \
    make -j5 && sudo make install && cd ..

RUN mkdir /data

WORKDIR /data


# change version of blackmagic video here
ADD Blackmagic_Desktop_Video_Linux_10.6.1 /data/blackmagicvideo

RUN apt-get update && apt-get install -y dkms libgl1-mesa-glx libxml2 
RUN apt-get update && apt-get install -y linux-headers-3.16.0-4-amd64


RUN cd /data/blackmagicvideo/deb/amd64 && sudo dpkg -i desktopvideo_*.deb && \
    cd ../../.. && rm -rf blackmagicvideo 

