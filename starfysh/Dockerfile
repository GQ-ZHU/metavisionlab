#tag:latest
# 基础镜像
FROM pytorch/pytorch:2.0.0-cuda11.7-cudnn8-runtime

# 安装系统依赖
RUN apt-get update && apt-get install -y \
    build-essential \
    gfortran \
    && rm -rf /var/lib/apt/lists/*

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

# 设置工作目录
WORKDIR /workspace

RUN /opt/conda/bin/conda init bash
