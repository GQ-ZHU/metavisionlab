#tag:latest
FROM pytorch/pytorch:2.5.0-cuda12.1-cudnn9-runtime
RUN python --version
RUN python3 --version

RUN apt-get update && apt-get install -y \
    curl nano psmisc zip git build-essential && \
    apt-get --fix-broken install -y && \
    rm -rf /var/lib/apt/lists/*

RUN conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/ && \
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ && \
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/ && \
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/rapidsai/ && \
    conda config --set show_channel_urls yes
    
# 安装 mkl & gdal
RUN conda install -y mkl mkl-service && \
    conda install -c conda-forge -y gdal=3.11.3

# 安装 Histomicstk
RUN pip install "histomicstk>=1.2.0" \
    --find-links https://girder.github.io/large_image_wheels \
    -i https://pypi.tuna.tsinghua.edu.cn/simple

# 安装Starfysh
# Step 1: Clone the Repository
WORKDIR /app
RUN git clone https://github.com/azizilab/starfysh.git
# Step 2: Navigate to the Repository
WORKDIR /app/starfysh
# Step 3: Install the Package
RUN pip install -r requirements.txt

# 安装 其他工具库
RUN pip install tensorboard scanpy squidpy scikit-learn matplotlib seaborn pandas numpy scipy statsmodels tangram-sc

RUN mamba install -c rapidsai -c conda-forge -c nvidia rapids=25.08 python=3.11 'cuda-version>=12.0,<=12.9'

# 初始化 conda
RUN /opt/conda/bin/conda init bash
