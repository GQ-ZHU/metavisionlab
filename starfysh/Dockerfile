#tag:latest
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# Step 0: 更新系统库并安装常用工具 + 添加 UbuntuGIS PPA 获取新版 GDAL
RUN apt-get update && apt-get install -y software-properties-common && \
    add-apt-repository ppa:ubuntugis/ppa && \
    apt-get update && apt-get install -y \
        libgl1-mesa-glx libpci-dev curl nano psmisc zip git \
        gdal-bin libgdal-dev \
    && apt-get --fix-broken install -y && \
    apt-get clean

# 设置工作目录
WORKDIR /app

# Step 1: Clone the Repository
RUN git clone https://github.com/azizilab/starfysh.git

# Step 2: Navigate to the Repository
WORKDIR /app/starfysh

# Step 3: Install the Package
RUN pip install .

# 升级 pip 和 setuptools，并安装常用 Python 库
RUN pip install pip==24.0 && python -m pip install --upgrade setuptools && \
    pip install \
    transformers \
    openai \
    scikit-learn \
    Pillow \
    numpy \
    matplotlib \
    seaborn \
    openpyxl \
    git+https://github.com/openai/CLIP.git

# 初始化 conda
RUN /opt/conda/bin/conda init bash
