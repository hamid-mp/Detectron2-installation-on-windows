
# Detectron2 installation on Windows

After Several days of confusion in installing Detectron2 on windows, I finally installed it. So here I've decided to show you the path that I went through.




## 🛠 Pycocotools
pycocotools is a Python API that assists in loading, parsing and visualizing the annotations in COCO.


but berfore installing `pycocotools`, first you should install 
`Visual Studio Build Tools 2019 (vs_BuildTools.exe)`

Follow the instructions that is presented in image below
![Follow the instruction](/pRpx0.png)

To install pycocotools, the recommended command is:
```bash
    pip install pycocotools
```

## 🛠 Installation

First , the Detectron2 repository must be downloaded from [here](https://github.com/facebookresearch/detectron2)
or simply use:
```bash
    git clone https://github.com/facebookresearch/detectron2.git
```
Next, changes must be made in **5 files** which their names are in following paths:
- `local_path/detectron2/utils/collect_env.py`
- `local_path/detectron2/engine/defaults.py`
- `local_path/detectron2/evaluation/evaluator.py`
- `local_path/detectron2/layers/csrc/cocoeval/cocoeval.cpp`
- `local_path/detectron2/layers/csrc/nms_rotated/nms_rotated_cuda.cu`
Please **replace** the modified files in this repo with yours. 

Use this command to install Detectron2
```bash
    cd detectron2
    pip install -e .
```
* Check the installation:
```bash
    python -m detectron2.utils.collect_env
```
The result should be like this:
![Follow the instruction](/result.JPG)

## 🛠 Correct unix paths
There is one more thing to do. we should refine unix paths which are `/` to windows `\`, we 
* __step1__ :
 download `iopath`:
```bash
git clone https://github.com/facebookresearch/iopath --single-branch --branch v0.1.8
```
* __step 2__:  
open `iopath/iopath/common/file_io.py` 
file, in class `HTTPURLHandler` and it's `_get_local_path` method,  in line 753 replace:
* `filename = path.split("/")[-1]`

with:
* `filename = parsed_url.path.split("/")[-1]`


* __step 3__ :  
Open a terminal with administrator premission, go to your local `iopath` repository and run following command:

```bash
pip install -e iopath
```

Hope you can use these instructions to easily install Detectron2. To get more information, follow the links.


## Links

- [pycocotool resolve](https://stackoverflow.com/questions/67940561/troubleshooting-pycocotools-installation)
- [Detectron2 Installation](https://ivanpp.cc/detectron2-walkthrough-windows/#step3installdetectron2)


## Authors

- [@Mohammad-Ali Mahmoodpour](https://github.com/hamid-mp)
- [@Mohammad-Javad Mirshekari](https://github.com/mj-haghighi)

