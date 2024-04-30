FROM condaforge/mambaforge
ARG DEBIAN_FRONTEND=noninteractive

#Update and install extra tools.
RUN apt-get -y update && apt-get -y install graphviz plantuml git software-properties-common

# Unfortunately mambaforge is still on ubuntu:focal, which means qt6 isn't available there
RUN add-apt-repository ppa:okirby/qt6-backports
RUN apt-get update && apt-get -y install xterm qt6-base-dev libxcb-cursor0

# Use this to debug x11 etc
# then do an ldd on the library which reports an error
#ENV QT_DEBUG_PLUGINS=1

#mamba update and emsvaltool
RUN mamba update -y conda mamba pip && mamba create -y --name datatools 

#set conda env
SHELL ["conda", "run", "--name", "datatools", "/bin/bash", "--login", "-c"]

#base tools tools
RUN mamba install -c conda-forge ipython gcc gfortran gdb make cmake libtool h5py udunits2 && conda clean --all -y


# We need to use pip to get exactly the versions we need. Hopefuly we wont need this from June 2024
RUN pip install git+https://github.com/davidhassell/cfdm@h5-read-0
RUN pip install git+https://github.com/davidhassell/cf-python@active-storage-0
RUN pip install pyqt6
ARG CACHE_BUSTER=1
RUN pip install git+https://github.com/ncas-cms/cf-view@qt6

#nuke dash
RUN rm /bin/sh&&ln -s /bin/bash /bin/sh

ENV PYTHONNOUSERSITE=1

RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc&&echo "conda activate datatools" >> ~/.bashrc
