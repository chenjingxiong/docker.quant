
# FROM jupyter/scipy-notebook
FROM jupyter/base-notebook

USER root
RUN apt-get update -y 
RUN apt-get install -y file apt-utils

RUN apt-get install -y gcc
RUN apt-get install -y make

RUN mkdir /tmp/quant
COPY ./ta-lib-0.4.0-src.tar.gz /tmp/quant

WORKDIR /tmp/quant
RUN pwd && tar -zxvf ta-lib-0.4.0-src.tar.gz && \
    cd ta-lib && \
    ./configure && make && \
    sudo make install

COPY ./requirements.txt /tmp/quant
RUN conda install -y --file /tmp/quant/requirements.txt

WORKDIR /tmp/quant
RUN conda install -y lxml pandas requests

RUN apt-get install -y git

RUN cd /tmp/quant && \
    git clone https://github.com/QuantFans/quantdigger.git

RUN pip install bs4 && \
    pip install tushare

RUN cd /tmp/quant/quantdigger && \
    sh install.sh

RUN pip install bt && conda info -e

USER jovyan

WORKDIR /home/jovyan
