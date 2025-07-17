# pytorch-cuda

Inside the Jetson nano
```bash
sudo apt install python3-pip
```

Enter into the Docker
```bash
docker compose run --rm jetson
```

Inside the docker execute the following to install pyenv:
```bash
sudo apt install -y curl && \
curl -fsSL https://pyenv.run | bash
```

Add pyenv to .bashrc
```bash
grep -F 'export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init - bash)"' $HOME/.bashrc || echo 'export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init - bash)"' >> $HOME/.bashrc
```

Source .bashrc
```bash
source .bashrc
```

Add pyenv to .profile
```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile && \
echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile && \
echo 'eval "$(pyenv init - bash)"' >> ~/.profile
```

Source .profile
```bash
source .profile
```

Install dependencies
```bash
sudo apt-get update
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python3-openssl git
```

Use pyenv to install in the container the same python version of the host
```bash
pyenv install 3.6.9
```

Create the venv and activate it
```bash
mkdir -p $HOME/python && cd $HOME/python && pyenv local 3.6.9 && python -m venv venv-3-6-9 && source venv-3-6-9/bin/activate
```

## Install Pythorch

Install [pytorch](https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048) v1.10 with CUDA support
```bash
wget https://nvidia.box.com/shared/static/fjtbno0vpo676a25cgvuqc1wty0fkkg6.whl -O torch-1.10.0-cp36-cp36m-linux_aarch64.whl
sudo apt-get install python3-pip libopenblas-dev libopenmpi-dev libomp-dev
pip3 install 'Cython<3'
pip3 install numpy torch-1.10.0-cp36-cp36m-linux_aarch64.whl
```

Install torchvision v0.11.1
```bash
sudo apt-get install libjpeg-dev zlib1g-dev libpython3-dev libopenblas-dev libavcodec-dev libavformat-dev libswscale-dev
git clone --branch release/0.11 https://github.com/pytorch/vision torchvision    
cd torchvision
export BUILD_VERSION=0.11.1  
python3 setup.py install --user
cd ../  
pip install 'pillow<7' # always needed for Python 2.7, not needed torchvision v0.5.0+ with Python 3.6
```
