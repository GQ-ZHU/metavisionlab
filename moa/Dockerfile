#tag:latest
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 更新系统库，安装常用工具
RUN apt-get update && apt-get install -y \
    libgl1-mesa-glx libpci-dev curl nano psmisc zip git && \
    apt-get --fix-broken install -y

# # MoA 项目
# 设置工作目录
WORKDIR /app
# 克隆 MoA 仓库
RUN git clone https://github.com/cvlab-kaist/MoA.git
WORKDIR /app/MoA
# 安装 Python 依赖
RUN pip install --no-cache-dir -r requirements.txt

RUN pip install pip==24.0 && python -m pip install --upgrade setuptools
RUN /opt/conda/bin/conda init bash
