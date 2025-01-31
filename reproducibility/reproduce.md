# **Repositories**

[Original Repository](https://github.com/FDUDSDE/MAGIC)  
[PIDDL Repository](https://github.com/PIDDL/MAGIC)  
[My Fork](https://github.com/m-shayan73/MAGIC/tree/reproduce)

# **Setup**

1) Clone the repository.

2) To setup the environment we have used Anaconda 24.9.1. For installation follow the instructions [here](https://docs.anaconda.com/anaconda/install/):

3) Run the following commands (inside conda) to create and run the environment required for MAGIC:

    ```
    conda create -n magic_env python=3.8
    conda activate magic_env
    ```
    
4) Install all the dependencies:

    ```
    conda install pytorch==1.12.0 torchvision==0.13.0 torchaudio==0.12.0 cudatoolkit=11.6 xxhash scikit-learn==1.2.2 -c pytorch -c conda-forge
    
    wget -O ./dgl.tar.bz2 https://anaconda.org/dglteam/dgl/1.0.0.cu116/download/linux-64/dgl-1.0.0.cu116-py38_0.tar.bz2
    conda install ./dgl.tar.bz2
    rm ./dgl.tar.bz2

    conda install -y networkx psutil requests tqdm
    ```

5) Alternatively, we have provided a [Dockerfile](./Dockerfile) for ease.

    1) Docker build:

        ```
        docker build -t magic .
        ```

    2) Navigate to the downloaded / cloned MAGIC repository and run the following command to start the container with the current directory (i.e. MAGIC's repository) mounted (inside the workspace folder of the container)

        ```
        docker run -it -v "$(pwd)":/workspace magic
        ```

    3) To find the current / mounted directory inside the container:

        ```
        cd workspace
        ```

6) Follow the instructions mentioned in [MAGIC's readme](https://github.com/FDUDSDE/MAGIC) to download the datasets and run the code.

