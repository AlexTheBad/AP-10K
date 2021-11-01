<h1 align="left">AP-10K: A Benchmark for Animal Pose Estimation in the Wild <a href="https://arxiv.org/abs/2108.12617"><img  src="https://img.shields.io/badge/arXiv-Paper-<COLOR>.svg" ></a>
</a> </h1> 

<p align="center">
  <a href="#introduction">Introduction</a> |
  <a href="#Updates">Updates</a> |
  <a href="#Overview">Overview</a> |
  <a href="#download">Download</a> |
  <a href="#training-code">Training Code</a>
</p>

## Introduction

<p align="left">This repository is the official contains the introduction, annotation files, and code for the dataset AP-10K, which is the first large-scale dataset for general animal pose estimation. AP-10K consists of 10,015 images collected and filtered from 23 animal families and 54 species, with high-quality keypoint annotations. We also contain another about 50k images with family and species labels. The dataset can be used for supervised learning, cross-domain transfer learning, and intra- and inter-family domain. It can also be used in self-supervised learning, semi-supervised learning, etc. The annotation files are provided following the COCO style. </p>

## Updates

***01/11/2021***
We have uploaded the corresponding code and pretrained models for the usage of AP-10K dataset!

***01/11/2021***
We have updated the dataset! It now has 54 species for training!

***01/11/2021***
The AP-10K dataset is integrated into <a href='https://github.com/open-mmlab/mmpose/blob/master/docs/tasks/2d_animal_keypoint.md#ap-10k'>mmpose</a>! Please enjoy it!

***31/08/2021***
The paper is post on <a href="https://arxiv.org/abs/2108.12617">arxiv</a>! We have uploaded the annotation file!

## Overview

### keypoint definition

<p align="center">
<img src="images/keypointDef.jpg" width="400">
</p>

<table div align=center>
<thead>
  <tr>
    <th>Keypoint</th>
    <th>Description</th>
    <th>Keypoint</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>1</td>
    <td>Left Eye</td>
    <td>2</td>
    <td>Right Eye</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Nose</td>
    <td>4</td>
    <td>Neck</td>
  </tr>
  <tr>
    <td>5</td>
    <td>Root of Tail</td>
    <td>6</td>
    <td>Left Shoulder</td>
  </tr>
  <tr>
    <td>7</td>
    <td>Left Elbow</td>
    <td>8</td>
    <td>Left Front Paw</td>
  </tr>
  <tr>
    <td>9</td>
    <td>Right Shoulder</td>
    <td>10</td>
    <td>Right Elbow</td>
  </tr>
  <tr>
    <td>11</td>
    <td>Right Front Paw</td>
    <td>12</td>
    <td>Left Hip</td>
  </tr>
  <tr>
    <td>13</td>
    <td>Left Knee</td>
    <td>14</td>
    <td>Left Back Paw</td>
  </tr>
  <tr>
    <td>15</td>
    <td>Right Hip</td>
    <td>16</td>
    <td>Right Knee</td>
  </tr>
  <tr>
    <td>17</td>
    <td>Right Back Paw</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

### Annotations Overview
<p align="center">
<img src="images/Overview_species1.jpg" width="380" height='430'><img src="images/Overview_species2.jpg" width="380" height='430'>
</p>

## Download

The dataset and corresponding files can be downloaded from 

<a href='https://drive.google.com/file/d/1-FNNGcdtAQRehYYkGY1y4wzFNg4iWNad/view?usp=sharing'>[Google Drive]</a> <a href='https://pan.baidu.com/s/1tBGHjHIjDBV9Wcwy_Y2pkw'>[Baidu Pan]</a> (code: 6uz6)

(Optional) The full version with both labeled and unlabeled images can be downloaded with the script provided here 

<a href='https://drive.google.com/file/d/1aIZwekaVa2AhaDPXOHD9MVaoFHU65vhJ/view?usp=sharing'>[Google Drive]</a> <a href='https://pan.baidu.com/s/1rvOSfaHKGG5F7XafGyAe3w'>[Baidu Pan]</a> (code: a8yf)


## Training Code

Here we provide the example of training models with the AP-10K dataset. The code is based on the <a href='https://github.com/open-mmlab/mmpose/blob/master/docs/tasks/2d_animal_keypoint.md#ap-10k'>mmpose</a> project. 


### Installation

Please refer to <a href='https://github.com/open-mmlab/mmpose/blob/master/docs/install.md'>install.md</a> for Installation.

### Dataset Preparation

Please download the dataset from the <a href='#download'>Download</a> Section, and please extract the dataset under the data folder, e.g.,

```
mkdir data
unzip ap-10k.zip -d data/
mv data/ap-10k data/ap10k
```

The extracted dataset should be looked like:

```text
AP-10K
├── mmpose
├── docs
├── tests
├── tools
├── configs
|── data
    │── ap10k
        │-- annotations
        │   │-- ap10k-train-split1.json
        │   |-- ap10k-train-split2.json
        │   |-- ap10k-train-split3.json
        │   │-- ap10k-val-split1.json
        │   |-- ap10k-val-split2.json
        │   |-- ap10k-val-split3.json
        │   |-- ap10k-test-split1.json
        │   |-- ap10k-test-split2.json
        │   |-- ap10k-test-split3.json
        │-- data
        │   │-- 000000000001.jpg
        │   │-- 000000000002.jpg
        │   │-- ...

```

### Inference

The checkpoints can be downloaded from [HRNet-w32](https://download.openmmlab.com/mmpose/animal/hrnet/hrnet_w32_ap10k_256x256-18aac840_20211029.pth), [HRNet-w48](https://download.openmmlab.com/mmpose/animal/hrnet/hrnet_w48_ap10k_256x256-d95ab412_20211029.pth), [ResNet-50](https://download.openmmlab.com/mmpose/animal/resnet/res50_ap10k_256x256-35760eb8_20211029.pth), [ResNet-101](https://download.openmmlab.com/mmpose/animal/resnet/res101_ap10k_256x256-9edfafb9_20211029.pth).

```python
python tools/test.py <CONFIG_FILE> <DET_CHECKPOINT_FILE>
```

### Training

```python
bash tools/dist_train.sh <CONFIG_FILE> <GPU_NUM>
```

For example, to train the HRNet-w32 model with 1 GPU, please run:

```python
bash tools/dist_train.sh configs/animal/2d_kpt_sview_rgb_img/topdown_heatmap/ap10k/hrnet_w32_ap10k_256x256.py 1
```


