FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 更新系统库，安装常用工具
RUN apt-get update && apt-get install -y \
    libgl1-mesa-glx libpci-dev curl nano psmisc zip git && \
    apt-get --fix-broken install -y
