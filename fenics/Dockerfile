FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && \
    apt install -y sudo build-essential ca-certificates coreutils curl environment-modules gfortran git gpg lsb-release python3 python3-distutils python3-venv unzip zip && \
    rm -rf /var/lib/apt/lists/*

# Add a non-root user and set a password for that user
RUN useradd -m -s /bin/bash ubuntu \
    && echo "ubuntu:password" | chpasswd

# Grant sudo privileges to the user
RUN mkdir -p /etc/sudoers.d
RUN echo "ubuntu ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/ubuntu

USER ubuntu
WORKDIR /home/ubuntu

RUN cd /home/ubuntu/ && \
    git clone -c feature.manyFiles=true https://github.com/spack/spack.git

ENV PATH="${PATH}:/home/ubuntu/spack/bin"

RUN spack install petsc@3.18.3 ~superlu-dist && \
    spack install py-petsc4py@3.18.3 

RUN spack install fenics@2019.1.0.post0

RUN curl -fsSL https://code-server.dev/install.sh | sh

RUN sudo apt update && \
    sudo apt install xfce4 xfce4-goodies -y && \
    sudo apt install xrdp -y && \
    sudo service xrdp restart

EXPOSE 3389


