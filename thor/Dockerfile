#tag:latest
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 安装系统依赖
RUN apt-get update && apt-get install -y \
    libgl1-mesa-glx libpci-dev curl nano psmisc zip git && \
    apt-get --fix-broken install -y && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# 创建工作目录
WORKDIR /app

# -------------------------------
# 创建 Python 3.9 的虚拟环境
# -------------------------------
# 创建一个名为 thor_env 的 conda 环境，指定 python=3.9
RUN conda create -y -n thor_env python=3.9

# 设置默认环境为 thor_env
# conda run 可在非交互 shell 执行命令
SHELL ["conda", "run", "-n", "thor_env", "/bin/bash", "-c"]

# -------------------------------
# 安装 Thor 项目
# -------------------------------
RUN git clone https://github.com/GuangyuWangLab2021/Thor.git
WORKDIR /app/Thor

# 在 thor_env 环境中安装依赖
RUN pip install --upgrade pip
RUN pip install ".[vis,analysis]"

# 加入 conda 初始化与自动激活命令
RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate thor_env" >> ~/.bashrc

# ---- 输出当前虚拟环境和 Python 版本（用于验证） ----
RUN echo "=== Environment check ===" && \
    conda info --envs && \
    echo "Current Python:" && \
    python --version && \
    echo "========================="

# ---- 设置默认启动命令 ----
CMD ["/bin/bash", "--login"]

# RUN apt-get update && apt-get install -y \
#     libgl1-mesa-glx libpci-dev curl nano psmisc zip git && \
#     apt-get --fix-broken install -y
    
# # Thor 项目
# # 设置工作目录
# WORKDIR /app
# # 克隆 Thor 仓库
# RUN git clone https://github.com/GuangyuWangLab2021/Thor.git
# WORKDIR /app/Thor
# # 安装 Python 依赖
# RUN pip install ".[vis,analysis]"

# RUN /opt/conda/bin/conda init bash
