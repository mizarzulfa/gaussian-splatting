# Gaussian Splatting for Windows

## Read First

This repo is intended to provide beginners with a step-by-step guide for installing, training, and exploring 3D Gaussian Splatting on Windows, without requiring extensive command-line knowledge. The process is simplified by utilizing Python VENV instead of an Anaconda environment

## Source
```sh
https://github.com/jonstephens85/gaussian-splatting-Windows

https://github.com/graphdeco-inria/gaussian-splatting
```

## Getting Started

To begin, jump to the [Installation Guide](#installation-guide) section below for detailed step-by-step instructions

## Installation Guide

## Hardware
- An NVIDIA GPU with 24GB VRAM or more. Preferably an RTX 3090 or better


1. **Clone this Repository**

    ```sh
    git clone https://github.com/graphdeco-inria/gaussian-splatting --recursive
    ```

# Create a Virtual Environment:
To create a new virtual environment, open your terminal/command prompt and navigate to the directory where you want to create it. Then, run the following command:

```sh
python -m venv specify_name

## activate the Virtual environment:
specify_name\Scripts\activate
```
Replace specify_name with the desired name for your virtual environment.


2. **Install Dependencies**

    - **CUDA Toolkit v11.8:** [Download CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit-archive)
    - **Python 3.10.9 or later:** [Python Downloads](https://www.python.org/downloads/)

    - **Visual Studio 2019 or newer** You can download and install it [here](https://visualstudio.microsoft.com/vs/older-downloads/). Make sure you add Desktop Development with C++ when installing
    - **COLMAP** - download [here](https://github.com/colmap/colmap/releases) -- add the lib folder to your PATH environment variable
    - **FFMPEG** - download [here](https://ffmpeg.org/download.html) -- add the lib folder to your PATH environment variable
    - **ImageMagick** - download [here](https://imagemagick.org/script/download.php) - optional


3. **Install Python Packages**

    ```sh
    SET DISTUTILS_USE_SDK=1
    pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
    pip install cuda-python==11.8.0
    pip install tqdm
    pip install ./submodules/simple-knn
    pip install ./submodules/diff-gaussian-rasterization
    pip install plyfile
    ```


## FFMPEG Command to extract images from video

```sh 
FFMPEG -i {path to video} -qscale:v 1 -qmin 1 -vf fps={CHANGE THIS} %04d.jpg
```

## Preparing Images From Your Own Scenes 
create new folder called "input" then move image sequence inside that folder

 ```sh
<location>
|---input
    |---<image 0>
    |---<image 1>
    |---...
```

If you have COLMAP and ImageMagick on your system path, you can simply run

```sh
python convert.py -s <location> [--resize] #If not resizing, ImageMagick is not needed
```

## Optimizer
The optimizer uses PyTorch and CUDA extensions in a Python environment to produce trained models. These trained models are what you view in the real-time viewer. This is where you "processes your dataset" into 3D Guassian Splats.

## Running the Optimizer
```sh
python train.py -s <path to COLMAP or NeRF Synthetic dataset>
```

## Interactive Viewers

 ### Pre-built Windows Binaries
We provide pre-built binaries for Windows [here](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/binaries/viewers.zip). We recommend using them on Windows for an efficient setup, since the building of SIBR involves several external dependencies that must be downloaded and compiled on-the-fly.

Simply download the viewer.zip file from the links above and extract into your main dir

4. **Real-Time Viewer SIBR**

    ```sh
    <PATH>/viewers/bin/SIBR_gaussianViewer_app -m <path to trained model>
    ```
