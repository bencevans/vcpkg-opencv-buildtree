# vcpkg-opencv-buildtree

Building OpenCV with CuDNN Support on GitHub Actions takes too long. Times out after 6 hours. 🙏 GitHub, please add support for personal accounts to add larger hosted runners!

On AMD Ryzen 5 3600 6-Core Processor (Linux) takes ~1h45m.

## Linux

Ensure Docker is installed and up to date. Ran into issues with `apt update` which host Docker upgrade sorted.

On Host

```
mkdir vcpkg-build
cd vcpkg-build
docker run -it -v $(pwd):/mnt/persist nvidia/cuda:11.7.1-devel-ubuntu22.04
```

In Container

```
apt-get update
apt-get install -y git pkg-config python3 python3-distutils \
  libx11-dev libxft-dev libxext-dev libx11-dev \
  libxft-dev libxext-dev wget build-essential curl \
  zip unzip tar curl zip unzip tar bison libdbus-1-dev \
  libxi-dev libxtst-dev libcudnn8-dev libxrandr-dev

cd /mnt/persist/
git clone https://github.com/Microsoft/vcpkg.git
./vcpkg/bootstrap-vcpkg.sh
cd vcpkg/
./vcpkg install opencv4[dnn,cudnn]:x64-linux
```

## Windows

Install CUDA 11.7.1 + CuDNN

```
git clone https://github.com/Microsoft/vcpkg.git
./vcpkg/bootstrap-vcpkg.sh
cd vcpkg/
./vcpkg install opencv4[dnn,cudnn]:x64-windows-static-md
```
