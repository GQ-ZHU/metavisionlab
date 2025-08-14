#tag:latest
# Base image
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 安装系统工具
RUN apt-get update && apt-get install -y \
    zip git curl && \
    rm -rf /var/lib/apt/lists/*

# 升级 pip & setuptools
RUN pip install --upgrade pip setuptools wheel

# 使用 Conda 安装 GDAL 和 geopandas
RUN conda install -c conda-forge gdal=3.11.3 geopandas

# 克隆并安装 Starfysh
RUN git clone https://github.com/azizilab/starfysh.git /app/starfysh
WORKDIR /app/starfysh
RUN pip install .

