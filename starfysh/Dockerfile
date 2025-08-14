#tag:latest
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 更新 apt 并安装 gdal 相关依赖
RUN apt-get update && apt-get install -y \
    gdal-bin \
    libgdal-dev \
    && rm -rf /var/lib/apt/lists/*

# 升级 pip & setuptools
RUN pip install --upgrade pip setuptools wheel

# 克隆并安装
RUN git clone https://github.com/azizilab/starfysh.git /app/starfysh
WORKDIR /app/starfysh
RUN pip install .


RUN /opt/conda/bin/conda init bash
