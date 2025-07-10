#tag:latest
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 设置工作目录
WORKDIR /workspace

# 更新系统库，安装常用工具
RUN apt-get update && apt-get install -y \
    libgl1-mesa-glx libpci-dev curl nano psmisc zip git && \
    apt-get --fix-broken install -y

# 复制 Python 依赖文件到容器中
COPY requirements.txt .

# 安装 Python 依赖
RUN pip install --no-cache-dir -r requirements.txt

RUN pip install pip==24.0 && python -m pip install --upgrade setuptools

RUN /opt/conda/bin/conda init bash
