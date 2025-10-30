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
# 创建 Python 3.7 的虚拟环境
# -------------------------------
RUN conda create -y -n spec2mol python=3.7

# 设置默认环境为 spec2mol
# conda run 可在非交互 shell 执行命令
SHELL ["conda", "run", "-n", "spec2mol", "/bin/bash", "-c"]
RUN conda install rdkit -c rdkit
RUN conda install pytorch=1.6.0 torchvision -c pytorch

# 加入 conda 初始化与自动激活命令
RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate spec2mol" >> ~/.bashrc

# ---- 输出当前虚拟环境和 Python 版本（用于验证） ----
RUN echo "=== Environment check ===" && \
    conda info --envs && \
    echo "Current Python:" && \
    python --version && \
    echo "========================="

# ---- 设置默认启动命令 ----
CMD ["/bin/bash", "--login"]
