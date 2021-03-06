

# Deep Image Analogy

The major contributors of this repository include [Jing Liao](https://liaojing.github.io/html/index.html) and [Yuan Yao](http://yuanyao.info/).

## Introduction

**Deep Image Analogy** is initially described in the paper :

[Visual Attribute Transfer through Deep Image Analogy](https://arxiv.org/abs/1705.01088)

[Jing Liao](https://liaojing.github.io/html/index.html), [Yuan Yao](http://yuanyao.info/), [Lu Yuan](http://www.lyuan.org/), [Gang Hua](http://www.ganghua.org/), [Sing Bing Kang](http://www.singbingkang.com/publications/)

Microsoft Research & Shanghai Jiao Tong University

SIGGRAPH 2017

![image](https://github.com/msracver/Deep-Image-Analogy/blob/master/windows/deep_image_analogy/example/readme/teaser.png)



## Disclaimer

This is an official C++ combined with CUDA implementation of [Deep Image Analogy](https://arxiv.org/abs/1705.01088). It is worth noticing that:
- Our codes are based on Microsoft version [Caffe](https://github.com/Microsoft/caffe).
- Our codes only have been tested on Windows 10 and Windows Server with CUDA 8 or 7.5.
- Our codes only have been tested on several Nvidia GPU: Titan X, Titan Z, K40, GTX770.
- The size of input image is limited, mostly should not be large than 700x500 if you use 1.0 for parameter **ratio**.


## License

© Microsoft, 2017. Licensed under an  BSD 2-Clause license.

## Citation

```
  @article{liao2017visual,
    title={Visual Attribute Transfer through Deep Image Analogy},
    author={Liao, Jing and Yao, Yuan and Yuan, Lu and Hua, Gang and Kang, Sing Bing},
    journal={arXiv preprint arXiv:1705.01088},
    year={2017}
  }
```

## Application

### Photo to Style

One major application of our code is to transfer the style from a painting to a photo.
<div>
<img src="https://github.com/msracver/Deep-Image-Analogy/blob/master/windows/deep_image_analogy/example/readme/p2sface.gif"/>
</div>

### Style to Style

It can also swap the styles between two artworks.

![image](https://github.com/msracver/Deep-Image-Analogy/blob/master/windows/deep_image_analogy/example/readme/s2s.png)

### Style to Photo

The most challenging application is converting a sketch or a painting to a photo.

<img src = "https://github.com/msracver/Deep-Image-Analogy/blob/master/windows/deep_image_analogy/example/readme/s2p3.png">

<img src = "https://github.com/msracver/Deep-Image-Analogy/blob/master/windows/deep_image_analogy/example/readme/s2p4.png">

### Photo to Photo

It can do color transfer between two photos, such as generating time lapse.

![image](https://github.com/msracver/Deep-Image-Analogy/blob/master/windows/deep_image_analogy/example/readme/p2p.png)

## Getting Started

### Prerequisite

- Windows
- CUDA 8 or 7.5
- Visual Studio 2013
- cuDNN

### Build



- Build [Caffe](http://caffe.berkeleyvision.org/) at first. Just follow the tutorial [here](https://github.com/Microsoft/caffe).
- Edit ```deep_image_analogy.vcxproj``` under ```windows/deep_image_analogy``` to make the CUDA version in it match yours .
- Open solution ```Caffe``` and add ```deep_image_analogy``` project.
- Build project ```deep_image_analogy```.

### Download models

You need to download models VGG-19 model before start to run a demo. Go to ```windows/deep_image_analogy/models/vgg19/``` folder and download:
- http://www.robots.ox.ac.uk/~vgg/software/very_deep/caffe/VGG_ILSVRC_19_layers.caffemodel

### Demo

Open ```main.cpp``` in ```windows/deep_image_analogy/source/``` to see how to run a demo. You need to set several parameters which have been mentioned in the paper. To be more specific, you need to set

- **path_model**, where the VGG-19 model is.
- **path_A**, the input image A.
- **path_BP**, the input image BP.
- **path_output**, the output path.
- **GPU Number**, GPU ID you want to run this experiment.
- **Ratio**, the ratio to resize the inputs before sending them into the network.
- **Blend Weight**, the level of weights in blending process.
- **Output Ids**, IDs to name output files, mostly are the IDs of input A and input BP.
- **Flag of WLS Filter**, if you are trying to do photo style transfer, we recommend to switch this on to keep the structure of original photo.

### Direct Run

We also provide a pre-built executable file in folder ```windows/deep_image_analogy/exe/```, don't hesitate to try it.

To run this ```deep_image_analogy.exe```, you need to write a command line as:

```
deep_image_analogy.exe ../models/ ../demo/content.png ../demo/style.png ../demo/output/ 0 0.5 2 1 1 0
```

which means
- **path_model**=```../models/```
- **path_A**=```../demo/content.png```
- **path_BP**=```../demo/style.png```
- **path_output**=```../demo/output/```
- **GPU Number**=```0```
- **Ratio**=```0.5```
- **Blend Weight**=```2```
- **Output Ids**=```1 1```
- **Flag of WLS Filter**=```false```(```1``` means ```true```)

### Tips

- We often test images of size 600x400 and 448x448.
- For the sizes above, we set ratio to be 0.5 when the structure of the image is simple, such as face. And set ratio to be 1.0 on complicated examples like mountain, ship and garden.
- Blend weight controls the result appearance. If you want the result to be more like original content photo, please increase it; if you want the result more faithful to the style, please reduce it.
- For the four applications, our settings are mostly (but not definitely):
  - Photo2style: blend weight level-3, ratio-0.5 for face and ratio-1 for other cases.
  - Style2style: blend weight level-3, ratio-1.
  - Style2photo: blend weight level-2, ratio-0.5.
  - Photo2photo: blend weight level-3, ratio-1.

## Acknowledgments

Our codes acknowledge [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page), [PatchMatch](http://gfx.cs.princeton.edu/gfx/pubs/Barnes_2009_PAR/index.php), [lbfgs](https://github.com/jwetzl/CudaLBFGS) and [Caffe](https://github.com/BVLC/caffe). We also acknowledge to the authors of our image and style examples but we do not own the copyrights of them.
