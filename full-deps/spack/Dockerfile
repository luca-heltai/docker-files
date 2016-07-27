FROM dealii/ubuntu14

MAINTAINER luca.heltai@gmail.com

USER root

RUN apt-get update && apt-get install -yq \
    clang \
    curl \
    gfortran \
    git \
    environment-modules \
    unzip \
    wget

ADD spack/ $HOME/spack/
RUN mkdir $HOME/.spack

ADD compilers.yaml $HOME/.spack/
RUN chown -R $USER:$USER $HOME/spack/
RUN chown -R $USER:$USER $HOME/.spack/

ENV PATH $HOME/spack/bin/:$PATH
USER $USER

RUN spack install dealii@dev
