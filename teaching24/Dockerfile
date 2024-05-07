ARG BASE_CONTAINER=atmbnl/datatools

FROM $BASE_CONTAINER

LABEL author = "Bryan Lawrence"

USER root

RUN mamba install -c conda-forge jupyterlab notebook xarray

# make sure your command line and notebook can find ncdump and cfdump
ENV PATH=/opt/conda/envs/datatools/bin:/opt/conda/condabin:/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
