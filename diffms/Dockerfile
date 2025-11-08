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
# RUN conda create -y -c conda-forge -n diffms rdkit=2024.09.4 python=3.9
RUN conda install -y rdkit=2024.09.4

# 设置默认环境为 diffms
# conda run 可在非交互 shell 执行命令
# SHELL ["conda", "run", "-n", "diffms", "/bin/bash", "-c"]
# RUN pip install torch==2.3.1 torchvision==0.18.1 torchaudio==2.3.1 --index-url https://download.pytorch.org/whl/cu121

RUN git clone https://github.com/coleygroup/DiffMS.git
WORKDIR /app/DiffMS
RUN pip install --upgrade pip setuptools wheel
RUN pip install -e .

# 加入 conda 初始化与自动激活命令
# RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
#     echo "conda activate diffms" >> ~/.bashrc

# ---- 输出当前虚拟环境和 Python 版本（用于验证） ----
RUN echo "=== Environment check ===" && \
    conda info --envs && \
    echo "Current Python:" && \
    python --version && \
    echo "========================="

# ---- 设置默认启动命令 ----
# CMD ["/bin/bash", "--login"]
RUN /opt/conda/bin/conda init bash
