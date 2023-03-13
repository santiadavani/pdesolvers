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

# SPACK installation
RUN cd /usr/local/ && \
    git clone -c feature.manyFiles=true https://github.com/spack/spack.git

# Set PATH with spack
ENV PATH="${PATH}:/usr/local/spack/bin"

# Install petsc and py-petsc4py
RUN spack install petsc@3.18.3 ~superlu-dist && \
    spack install py-petsc4py@3.18.3 

# Set the user as the default user for the container
USER ubuntu
ENV PATH="${PATH}:/usr/local/spack/bin"

WORKDIR /home/ubuntu
RUN echo "source /usr/local/spack/share/spack/setup-env.sh" >> /home/ubuntu/.bashrc
CMD ["/bin/bash"]

