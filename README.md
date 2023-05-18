bRigNet
---------
Neural Rigging for [blender](https://www.blender.org/ "Blender Home Page") using [RigNet](https://zhan-xu.github.io/rig-net/ "RigNet Home Page")

This is an updated README to run bRigNet on Windows 10 21H2, CUDA 11.7, PyTorch 1.13.1 using Blender 2.90.1

Blender is the open source 3D application from the Blender Foundation. RigNet is the Machine Learning prediction
for articulated characters. It has a dual license, GPL3 for open source projects, commercial otherwise.
It was presented in the following papers

``` 
  @InProceedings{AnimSkelVolNet,
    title={Predicting Animation Skeletons for 3D Articulated Models via Volumetric Nets},
    author={Zhan Xu and Yang Zhou and Evangelos Kalogerakis and Karan Singh},
    booktitle={2019 International Conference on 3D Vision (3DV)},
    year={2019}
  }
```

```
  @article{RigNet,
    title={RigNet: Neural Rigging for Articulated Characters},
    author={Zhan Xu and Yang Zhou and Evangelos Kalogerakis and Chris Landreth and Karan Singh},
    journal={ACM Trans. on Graphics},
    year={2020},
    volume={39}
  }
```

## Setup

bRigNet requires SciPy, PyTorch and torch-geometric, along with torch-scatter and torch-sparse.

## Installation

Use Blender [2.90.1](https://download.blender.org/release/Blender2.90/) as the plugin does not work on newer versions.

Download the repoistory as a zip file and install it from the blender addons window. The RigNet submodule also have to be downloaded and insterted into the addon folder.

At present, the CUDA toolkit from nVidia is required, it can be found at the [manufacturer website](https://developer.nvidia.com).

```
nvcc --version
```

```
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2022 NVIDIA Corporation
Built on Wed_Jun__8_16:59:34_Pacific_Daylight_Time_2022
Cuda compilation tools, release 11.7, V11.7.99
Build cuda_11.7.r11.7/compiler.31442593_0
```

```
conda create -n brignet python=3.7
conda activate brignet
```

```
cd "%APPDATA%\Blender Foundation\Blender\2.90\scripts\addons\brignet-main"

virtualenv _additional_modules
cd _additional_modules
Scripts\activate

pip install torch==1.13.1+cu117 -f https://download.pytorch.org/whl/torch_stable.html
pip install torch-scatter -f https://pytorch-geometric.com/whl/torch-1.13.1+cu117.html
pip install torch-sparse -f https://pytorch-geometric.com/whl/torch-1.13.1+cu117.html
pip install torch-cluster -f https://pytorch-geometric.com/whl/torch-1.13.1+cu117.html
pip install torch-spline-conv -f https://pytorch-geometric.com/whl/torch-1.13.1+cu117.html
pip install torch-geometric==1.7.2
```

Enable *bRigNet* in the blender addons, the preferences will show up.

Set the Modules path properties to the RigNet environment from the previous step

RigNet requires a trained model. They have made theirs available at [this address](https://umass-my.sharepoint.com/:u:/g/personal/zhanxu_umass_edu/EYKLCvYTWFJArehlo3-H2SgBABnY08B4k5Q14K7H1Hh0VA). The checkpoint folder can be copied to the RigNet subfolder. A different location can be set in the addon preferences.

## Usage 

#### Rig Generation

the **bRigNet** tab will show up in the Viewport tools. Select a character mesh as target.
Please make sure it doesn't exceed the 5K triangles. You can use the *Decimator* modifier
to reduce the polycount on a copy of the mesh, and select a *Collection* of high res model
on which to transfer the final weights  

#### Load generated rigs

Rigs generated using RigNet from the command line can be loaded via the **Load Skeleton** panel.
Please select the *.obj and *.txt file and press the button **Load Rignet character**

## Training

The blender addon doesn't cover training yet. If you want to train your own model, please follow the instructions
from the [RigNet project](https://github.com/zhan-xu/RigNet#training).

## Disclaimer

This blender implementation of RigNet and the author of this add-on are NOT associated with the University of
Massachusetts Amherst.

This add-on has received a research grant from the Blender Foundation.   

## License

This addon is released under the GNU General Public License version 3 (GPLv3).
The RigNet subfolder is licensed under the General Public License Version 3 (GPLv3), or under a Commercial License.
