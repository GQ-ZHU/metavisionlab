#tag:latest
# 基础镜像
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 更新系统并安装依赖
RUN apt-get update && apt-get install -y \
    libgl1-mesa-glx \
    libpci-dev \
    curl \
    nano \
    psmisc \
    zip \
    git \
    wget \
    gdal-bin \
    libgdal-dev \
    python3-gdal \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# 升级 pip & setuptools
RUN pip install --upgrade pip setuptools wheel

# 安装 Python 依赖
RUN pip install \
    transformers \
    accelerate \
    openai \
    scikit-learn \
    Pillow \
    numpy \
    matplotlib \
    seaborn \
    openpyxl

# 克隆并安装 starfysh
WORKDIR /app
RUN git clone https://github.com/azizilab/starfysh.git
WORKDIR /app/starfysh
RUN pip install .

# 进入 bash 环境时初始化 conda
RUN /opt/conda/bin/conda init bash

