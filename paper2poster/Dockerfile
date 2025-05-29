#tag:latest
# 基础镜像
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 设置工作目录
WORKDIR /workspace

# 更新系统库，安装常用工具 + libreoffice（建议安装 headless 版本）
RUN apt-get update && \
    apt-get install -y \
    libgl1-mesa-glx libpci-dev curl nano psmisc zip git \
    libreoffice libreoffice-writer libreoffice-calc libreoffice-impress \
    && apt-get --fix-broken install -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 复制 Python 依赖文件到容器中
COPY requirements.txt .

# 安装 Python 依赖
RUN pip install --no-cache-dir -r requirements.txt

RUN /opt/conda/bin/conda init bash
