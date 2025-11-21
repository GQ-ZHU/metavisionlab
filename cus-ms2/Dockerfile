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
# 创建 Python 3.8 的虚拟环境
# -------------------------------
RUN conda create --name CSU-MS2 python=3.8.18

# 设置默认环境为 CSU-MS2
# conda run 可在非交互 shell 执行命令
SHELL ["conda", "run", "-n", "CSU-MS2", "/bin/bash", "-c"]

RUN git clone https://github.com/tingxiecsu/CSU-MS2.git
WORKDIR /app/CSU-MS2
RUN conda install --file requirements.txt

# 加入 conda 初始化与自动激活命令
RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate CSU-MS2" >> ~/.bashrc

# ---- 输出当前虚拟环境和 Python 版本（用于验证） ----
RUN echo "=== Environment check ===" && \
    conda info --envs && \
    echo "Current Python:" && \
    python --version && \
    echo "========================="

# ---- 设置默认启动命令 ----
CMD ["/bin/bash", "--login"]
# RUN /opt/conda/bin/conda init bash
