#tag:latest
FROM pytorch/pytorch:2.6.0-cuda12.4-cudnn9-runtime

# 更新系统库，安装常用工具
RUN apt-get update && apt-get install -y \
    libgl1-mesa-glx libpci-dev curl nano psmisc zip git && \
    apt-get --fix-broken install -y

RUN pip install pip==24.0 && python -m pip install --upgrade setuptools && \
    pip install \
    diffusers \
    accelerate \
    sentencepiece \
    protobuf \
    openai \
    scikit-learn \
    Pillow \
    numpy \
    matplotlib \
    seaborn \
    git+https://github.com/openai/CLIP.git

RUN /opt/conda/bin/conda init bash
