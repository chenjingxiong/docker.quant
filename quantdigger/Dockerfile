
FROM jupyter/scipy-notebook

USER root
RUN apt-get update -y  && apt-get install -y file

RUN mkdir /tmp/quant
COPY ./ta-lib-0.4.0-src.tar.gz /tmp/quant

WORKDIR /tmp/quant
RUN pwd && tar -zxvf ta-lib-0.4.0-src.tar.gz && \
    cd ta-lib && \
    ./configure && make && \
    sudo make install

COPY ./requirements.txt /tmp/quant
RUN pwd && conda create -y --name quant --file /tmp/quant/requirements.txt

RUN mv /bin/sh /bin/sh.bak && ln -sf /bin/bash /bin/sh

WORKDIR /tmp/quant
RUN pwd && . activate quant && \
    conda install -y lxml pandas requests

RUN pwd && . activate quant && \
    cd /tmp/quant && \
    git clone https://github.com/QuantFans/quantdigger.git

RUN pwd && . activate quant && \
    conda list && pip list && \
    pip install bs4 && \
    pip install tushare

RUN pwd && . activate quant && \
    cd /tmp/quant/quantdigger && \
    sh install.sh

RUN pwd && . activate quant && \
    conda list && pip list && \
    pip install bt

RUN rm /bin/sh && mv /bin/sh.bak /bin/sh

USER jovyan

WORKDIR /home/jovyan
