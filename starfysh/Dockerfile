#tag:latest
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime


ENV DEBIAN_FRONTEND=noninteractive

# 安装系统工具 + OpenJDK
RUN apt-get update && apt-get install -y \
    tzdata \
    zip git curl \
    openjdk-11-jdk \
    && rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH

# 升级 pip & setuptools
RUN pip install --upgrade pip setuptools wheel

RUN conda update -n base -c defaults conda -y
RUN conda install -c conda-forge gdal=3.11.3 -y


# 克隆并安装 Starfysh
RUN git clone https://github.com/azizilab/starfysh.git /app/starfysh
WORKDIR /app/starfysh
RUN pip install -r requirements.txt
RUN /opt/conda/bin/conda init bash
