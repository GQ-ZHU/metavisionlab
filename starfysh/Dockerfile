#tag:latest
# 基础镜像：PyTorch GPU 版 + CUDA 12.4
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 设置 Python 版本为 3.8
RUN conda install -y python=3.8 && conda clean -ya

# 安装常用系统依赖（opencv、scanpy、histomicstk 等需要）
RUN apt-get update && apt-get install -y \
    git \
    libgl1-mesa-glx \
    libglib2.0-0 \
    libgdal-dev \
    gdal-bin \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# 克隆 starfysh 项目
WORKDIR /app
RUN git clone https://github.com/azizilab/starfysh.git
WORKDIR /app/starfysh

# 安装 Python 依赖
RUN pip install --no-cache-dir .

RUN /opt/conda/bin/conda init bash
