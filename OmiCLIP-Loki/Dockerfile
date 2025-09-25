#tag:latest
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 更新系统库，安装常用工具
RUN apt-get update && apt-get install -y \
    libgl1-mesa-glx libpci-dev curl nano psmisc zip git && \
    apt-get --fix-broken install -y
    
# Loki 项目
# 设置工作目录
WORKDIR /app
# 克隆 Loki 仓库
RUN git clone https://github.com/GuangyuWangLab2021/Loki.git
WORKDIR /app/Loki/src
# 安装 Python 依赖
RUN pip install .
