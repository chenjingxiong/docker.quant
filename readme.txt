------------------------------------------------------------------------------------------
tk
Dockerfile
    quantdigger
    based on scipy-notebook
Dockerfile2, based on small base-notebook
    guantdigger

Dockerfile3
    based on small base-notebook, root env
    zipline & backtrader
    env quant

------------------------------------------------------------------
tk docker build

tk docker build
refer to :
https://hub.docker.com/r/jupyter/
https://hub.docker.com/r/jupyter/scipy-notebook/
docker pull jupyter/scipy-notebook

Quant :
backtest
    https://github.com/pmorissette/bt
tushare
    https://github.com/waditu/tushare
quantdigger
    https://github.com/andyzsf/quantdigger
    https://github.com/QuantFans/quantdigger

basic requires
requests>=2.18.1
BeautifulSoup4>=4.6
lxml>=3.8
tushare>=0.8.2
pyzmq>=4.1.5
six
logbook>=0.12.5
numpy>=1.13.1
pandas>=0.20.2
pymongo>=3.1.1
matplotlib>=1.5.1
python-dateutil>=2.4.2
progressbar2>=3.6.2
TA-Lib>=0.4.8

------------------------------------------------------------------------------------------
tk TA-lib install
https://mrjbq7.github.io/ta-lib/install.html
http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz
http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-msvc.zip
Download ta-lib-0.4.0-src.tar.gz and:

$ untar and cd
$ ./configure --prefix=/usr
$ make
$ sudo make install


------------------------------------------------------------------------------------------
tk run

make sure current folder contain 'work' sub-dir and start-notebook.sh in it

build image
    docker -l debug build -f Dockerfile -t quant .

run python notebook/jupyter/pandas

run python notebook/jupyter/pandas with quant environment

docker -l debug build -f Dockerfile -t quant .

docker run -it --rm -p 8888:8888 \
    -v /u01/save:/u01/save/ \
    -v ./work:/home/jovyan/work/ \
    --entrypoint /home/jovyan/work/start-notebook.sh \
    quant

docker run -it --rm -p 8889:8888 \
    -v /u01/save:/u01/save/ \
    -v ${PWD}/work:/home/jovyan/work/ \
    --entrypoint /home/jovyan/work/start-notebook.sh \
    quant


docker -l debug build -f Dockerfile3 -t quant.zipline .

docker run -it --rm -p 8889:8888 \
    -v /u01/save:/u01/save/ \
    -v /u01/save/work:/home/jovyan/work/ \
    quant.zipline

