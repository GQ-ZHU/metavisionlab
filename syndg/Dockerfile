#tag:latest
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 更新系统库，安装常用工具
RUN apt-get update && apt-get install -y \
    libgl1-mesa-glx libpci-dev curl nano psmisc zip git && \
    apt-get --fix-broken install -y

# # Dassl.pytorch 项目
# 设置工作目录
WORKDIR /app
# 克隆 Dassl.pytorch 仓库
RUN git clone https://github.com/KaiyangZhou/Dassl.pytorch.git
WORKDIR /app/Dassl.pytorch
# 安装 Python 依赖
RUN pip install tensorflow
RUN pip install --no-cache-dir -r requirements.txt
# 安装 Dassl.pytorch 库
RUN python setup.py develop


RUN pip install pip==24.0 && python -m pip install --upgrade setuptools && \
    pip install \
    transformers \
    diffusers \
    accelerate \
    sentencepiece \
    protobuf \
    openai \
    scikit-learn \
    Pillow \
    numpy \
    matplotlib \
    seaborn \
    openpyxl \
    git+https://github.com/openai/CLIP.git

RUN /opt/conda/bin/conda init bash
