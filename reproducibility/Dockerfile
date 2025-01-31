# Start with an official Ubuntu 24.04 base image (OS not mentioned in the paper or repository)
FROM ubuntu:24.04

# Set environment variables to prevent prompts during installations
ENV DEBIAN_FRONTEND=noninteractive

# Update and install required packages
RUN apt-get update && apt-get install -y \
    wget \
    bzip2 \
    zip \
    unzip \
    tar \
    && apt-get clean

# Download and install Anaconda
RUN wget https://repo.anaconda.com/archive/Anaconda3-2024.10-1-Linux-x86_64.sh -O /tmp/anaconda.sh && \
    bash /tmp/anaconda.sh -b -p /anaconda && \
    rm /tmp/anaconda.sh

# Set Anaconda path
ENV PATH="/anaconda/bin:$PATH"

# Create a Conda environment and install required libraries
RUN conda create -n magic_env python=3.8 -y && \
    conda run -n magic_env conda install -y \
    pytorch==1.12.0 \
    torchvision==0.13.0 \
    torchaudio==0.12.0 \
    cudatoolkit=11.6 \
    xxhash \
    scikit-learn==1.2.2 \
    -c pytorch -c conda-forge

# Download and install DGL with its dependencies - unable to install cuda version of DGL 1.0.0 directly via conda install
RUN wget -O /tmp/dgl.tar.bz2 https://anaconda.org/dglteam/dgl/1.0.0.cu116/download/linux-64/dgl-1.0.0.cu116-py38_0.tar.bz2 && \
    conda run -n magic_env conda install -y /tmp/dgl.tar.bz2 && \
    conda run -n magic_env conda install -y networkx psutil requests tqdm && \
    rm /tmp/dgl.tar.bz2 && \
    conda clean -a

# Set the default environment when running the container
ENV CONDA_DEFAULT_ENV=magic_env
ENV PATH="/anaconda/envs/magic_env/bin:$PATH"

# Set working directory
WORKDIR /workspace

# Default command
CMD ["bash"]