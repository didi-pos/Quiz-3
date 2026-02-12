FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
    python3-pip \
    git \
    libgl1-mesa-glx \
    mesa-utils \
    && rm -rf /var/lib/apt/lists/*
WORKDIR /app
RUN git clone https://github.com/rparak/PyBullet_Industrial_Robotics_Gym.git .
RUN pip3 install pybullet numpy matplotlib scipy pandas torch torchvision stable-baselines3 gymnasium
ENV PYTHONPATH=/app/src:$PYTHONPATH
CMD ["python3", "Evaluation/PyBullet/Environment/test_env.py"]
