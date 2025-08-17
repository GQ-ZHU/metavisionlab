#tag:latest
# 基础镜像
FROM pytorch/pytorch:1.13.0-cuda11.6-cudnn8-runtime

# 安装系统依赖
RUN apt-get update && apt-get install -y \
    build-essential \
    gfortran \
    git \
    curl \
    openjdk-11-jdk \
    && rm -rf /var/lib/apt/lists/*

# 设置 JAVA_HOME 环境变量
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH

# 用 conda 安装 MKL
RUN conda install -y mkl mkl-service

# 升级 pip
RUN pip install --upgrade pip

# 安装指定 Python 库
RUN pip install \
    numpy==1.22.1 \
    pandas \
    pymc3 \
    scanpy \
    setuptools==58.0.0 \
    wheel==0.36.2

RUN pip install histomicstk --find-links https://girder.github.io/large_image_wheels -i https://pypi.tuna.tsinghua.edu.cn/simple

# 使用 Conda 安装 GDAL
# RUN conda install -c conda-forge gdal=3.11.3

# 安装Starfysh
RUN pip install Starfysh


# # Step 1: Clone the Repository
# WORKDIR /app
# RUN git clone https://github.com/azizilab/starfysh.git

# # Step 2: Navigate to the Repository
# WORKDIR /app/starfysh

# # Step 3: Install the Package
# RUN pip install -r requirements.txt

# # 设置工作目录
# WORKDIR /workspace

RUN /opt/conda/bin/conda init bash
