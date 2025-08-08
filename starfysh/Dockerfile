#tag:latest
# 基础镜像
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 更新系统库并安装构建工具
RUN apt-get update && apt-get install -y \
    software-properties-common \
    build-essential \
    curl \
    libgl1-mesa-glx \
    libpci-dev \
    nano \
    psmisc \
    zip \
    git \
    ca-certificates \
    wget \
    unzip \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# ----------------------------------------------------------
# 安装 GDAL 3.11.3 (源码编译)
# ----------------------------------------------------------
WORKDIR /tmp

# 下载 GDAL 源码
RUN wget https://download.osgeo.org/gdal/3.11.3/gdal-3.11.3.tar.gz && \
    tar -xvzf gdal-3.11.3.tar.gz && \
    cd gdal-3.11.3 && \
    ./configure --prefix=/usr --with-python && \
    make -j$(nproc) && \
    make install && \
    ldconfig && \
    cd .. && rm -rf gdal-3.11.3*

# 设置环境变量（让 pip 安装 gdal 能找到头文件）
ENV CPLUS_INCLUDE_PATH=/usr/include/gdal
ENV C_INCLUDE_PATH=/usr/include/gdal

# ----------------------------------------------------------
# 克隆并安装 starfysh 项目
# ----------------------------------------------------------
WORKDIR /app
RUN git clone https://github.com/azizilab/starfysh.git
WORKDIR /app/starfysh

# 升级 pip & 安装依赖
RUN pip install --upgrade pip setuptools wheel
RUN pip install .

# ----------------------------------------------------------
# 额外安装常用 Python 库
# ----------------------------------------------------------
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

# ----------------------------------------------------------
# 默认工作目录
# ----------------------------------------------------------
WORKDIR /app

# 初始化 conda
RUN /opt/conda/bin/conda init bash
