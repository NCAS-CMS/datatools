FROM condaforge/mambaforge

#Update and install extra tools.
RUN apt-get -y update && DEBIAN_FRONTEND=noninteractive apt-get -y install qt5-default graphviz plantuml

#mamba update and emsvaltool
RUN mamba update -y conda mamba pip && mamba create -y --name datatools esmvaltool-python

#set conda env
SHELL ["conda", "run", "--name", "datatools", "/bin/bash", "--login", "-c"]

#cf-python and other tools
RUN mamba install -c conda-forge cf-python cf-plot ipython gcc gfortran gdb make cmake libtool && conda clean --all -y
RUN pip install cf-view #Not yet in conda

#nuke dash
RUN rm /bin/sh&&ln -s /bin/bash /bin/sh

ENV PYTHONNOUSERSITE=1

RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc&&echo "conda activate datatools" >> ~/.bashrc
