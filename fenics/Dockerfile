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

# Set the user as the default user for the container
USER ubuntu
WORKDIR /home/ubuntu

#Update
CMD ["/bin/bash"]

