FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# Step 1: 更新系统库并安装工具
RUN apt-get update && apt-get install -y \
    curl nano psmisc zip git build-essential && \
    apt-get --fix-broken install -y && \
    rm -rf /var/lib/apt/lists/*

# Step 2: 创建 conda 环境 (Python 3.9)
RUN conda create -y -n starfysh python=3.9 && \
    echo "conda activate starfysh" >> ~/.bashrc

# Step 3: 安装依赖库
SHELL ["conda", "run", "-n", "starfysh", "/bin/bash", "-c"]

# 安装 mkl & gdal
RUN conda install -y mkl mkl-service && \
    conda install -c conda-forge -y gdal=3.11.3

# 安装 Histomicstk
RUN pip install "histomicstk>=1.2.0" \
    --find-links https://girder.github.io/large_image_wheels \
    -i https://pypi.tuna.tsinghua.edu.cn/simple

# 安装 PyTorch 2.5.0 (CUDA 12.1 版本)
RUN conda install -y pytorch==2.5.0 torchvision==0.20.0 torchaudio==2.5.0 pytorch-cuda=12.1 -c pytorch -c nvidia

# 设置默认进入 conda 环境
ENTRYPOINT [ "conda", "run", "--no-capture-output", "-n", "starfysh", "bash" ]
