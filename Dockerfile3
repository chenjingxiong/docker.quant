FROM jupyter/base-notebook
# FROM jupyter/scipy-notebook

USER root

RUN apt-get update -y  && apt-get install -y file apt-utils

RUN pwd && conda create -y --name quant -c quantopian zipline python=3.4

RUN mv /bin/sh /bin/sh.bak && ln -sf /bin/bash /bin/sh

RUN pwd && . activate quant && \
    conda install -y lxml pandas requests

RUN pwd && . activate quant && \
    pip install backtrader && \
    pip install backtrader[plotting]

RUN rm /bin/sh && mv /bin/sh.bak /bin/sh

RUN mkdir /home/jovyan/bin

COPY ./work/start-notebook.sh /home/jovyan/bin

RUN pwd && conda install -y --name quant notebook jupyter

# RUN wget --quiet https://github.com/krallin/tini/releases/download/v0.10.0/tini && \
#     echo "1361527f39190a7338a0b434bd8c88ff7233ce7b9a4876f3315c22fce7eca1b0 *tini" | sha256sum -c - && \
#     mv tini /usr/bin/tini && \
#     chmod +x /usr/bin/tini

# ENTRYPOINT ["/usr/bin/tini" "--"]
CMD ["/home/jovyan/bin/start-notebook.sh"]

USER jovyan
WORKDIR /home/jovyan


