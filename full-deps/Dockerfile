FROM tjhei/dealii-base

MAINTAINER timo.heister@gmail.com

USER root
RUN apt-get update && sudo apt-get -yq install \
    gcc \
    clang \
    g++ \
    gfortran \
    libblas-dev \
    liblapack-dev \
    libopenmpi-dev \
    openmpi-bin \
    cmake \
    git \
    wget \
    python \
    numdiff \
    ninja-build
USER bob

USER root
ADD candi/ $HOME/candi/
RUN chown -R bob:bob $HOME/candi/
USER bob

RUN \
  cd candi; \
  ./candi.sh -j4 --prefix=~/libs --packages="load:dealii-prepare once:opencascade once:parmetis once:hdf5 once:p4est once:trilinos once:petsc once:slepc"

# I don't know how to import env vars from the configuration folder.  This
# probably doesn't work at all, because we don't use bash but sh and so we can
# not use 'source' or any of the bash startup files. Manually export the paths
# here instead:
RUN cat ~/libs/configuration/* | grep export

ENV HDF5_DIR=/home/bob/libs/hdf5-1.8.15-patch1
ENV OPENCASCADE_DIR=/home/bob/libs/oce-OCE-0.17
ENV METIS_DIR=/home/bob/libs/parmetis-4.0.3
ENV PARMETIS_DIR=/home/bob/libs/parmetis-4.0.3
ENV PETSC_DIR=/home/bob/libs/petsc-3.6.4
ENV SLEPC_DIR=/home/bob/libs/slepc-3.6.0
ENV TRILINOS_DIR=/home/bob/libs/trilinos-12.4.2-Source
ENV P4EST_DIR=/home/bob/libs/p4est-1.1

RUN rm -rf ~/candi ~/libs/tmp
