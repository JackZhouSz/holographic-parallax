# Holographic Parallax Improves 3D Perceptual Realism
### [Paper](https://dl.acm.org/doi/10.1145/3658168) | [arXiv](https://arxiv.org/abs/2404.11810) | [Project Page](https://www.computationalimaging.org/publications/holographic-parallax/) | [Video](https://youtu.be/p43MSDOEWWw?si=2VC_8LeOhYAUm2Et)

[Dongyeon Kim*](https://dongyeon93.github.io/),
[Seung-Woo Nam*](https://nseungwoo.github.io/),
[Suyeon Choi*](https://choisuyeon.github.io/),
[Jong-Mo Seo](),
[Gordon Wetzstein](https://stanford.edu/~gordonwz/),
and [Yoonchan Jeong](http://oeqelab.snu.ac.kr/) (\* denotes equal contribution)

Source code for the SIGGRAPH 2024 paper titled "Holographic Parallax Improves 3D Perceptual Realism"

This is an updated version of [Time-multiplexed-neural-holography](https://github.com/computational-imaging/time-multiplexed-neural-holography), now including additional features relevant to binary amplitude SLMs and incoherent focal stack generation from a RGB-depthmap and orthographic views.

## Get Started
Create anaconda environment. 
Our code has been implemented and tested on Windows.

```
conda env create -f environment.yml
conda activate holographic-parallax
```

## Target RGB-D, and light field
We use the inputs of RGB-depthmap, or light field (orthographic views).
We provide a sample RGB-D map and [light field](https://drive.google.com/drive/folders/1SD5bGaiIzJZ3cXgStAbrZD2YVArM1x3j?usp=sharing) of [Stanford Bunny and Dragon](http://graphics.stanford.edu/data/3Dscanrep/) rendered with Unity. 
Place the `lf_dataset` into the `data` folder.

The sample RGB-D and 25x25x3 light field map are rendered based on parameters from 'flcos' SLM and 'wiki' light_src explained in `params.py`. 
The image resolution is reduced to (900, 1600), and angle spacing is adjusted depending on the color channel.

## Focal stack generation
### Focal stack from RGB-D (Target for 3D w/ RGB-D)
```
# focal stack generation mode test cmd
python Incoherent_focal_stack.py --config_filepath=./configs/gen_lf.txt
```
This will scan a pair of images from `./data/rgbd_dataset` folder: `{image_name}_depthmap.png`, `{image_name}_rgb.png`.
Then, it will create focal stack from a single RGB-D in `./data/fs_dataset/{image_name}/ch_{channel}`.

### Focal stack from dense light field (Target for 3D w/ LF)
```
# light field focal stack generation mode test cmd
python Incoherent_LF_focal_stack.py --config_filepath=./configs/gen_fs_lf.txt
```
Note that the configuration file has to be changed with proper {image_name}, {channel}.
This will create a focal stack from 25x25 dense light field in `./data/lf_fs_dataset/{image_name}/ch_{channel}`.

## CGH optimization
2.5D
```
# 2.5D supervision
bash ./configs/2.5d_rgb_bash.sh
```

3D w/ RGB-D
```
# 3D supervision
bash ./configs/3d_rgb_bash.sh
```

3D w/ LF
```
# 3.5D supervision
bash ./configs/3.5d_rgb_bash.sh
```

4D supervision
```
# 4D supervision
bash ./configs/4d_rgb_bash.sh
```

## Acknowledgements
We acknowledge that the implementation of our code was mostly forked from [Time-multiplexed-neural-holography](https://github.com/computational-imaging/time-multiplexed-neural-holography). 
Several features are updated to suit our holographic display setup with binary amplitude SLM. 
Additionally, our method for generating the incoherent focal stack from RGB-depthmap images is based on the approach described in the work of [Lee et al.](https://doi.org/10.1038/s41598-022-06405-2).

## Citation
```
@article{kim2024holographic,
title={Holographic Parallax Improves 3D Perceptual Realism},
author={Kim, Dongyeon and Nam, Seung-Woo and Choi, Suyeon and Seo, Jong-Mo and Wetzstein, Gordon and Jeong, Yoonchan},
journal={ACM Transactions on Graphics (TOG)},
volume={43},
number={4},
articleno = {68},
pages={1–13},
year={2024},
publisher={ACM New York, NY, USA}
}
```
