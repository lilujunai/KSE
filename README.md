# Exploiting Kernel Sparsity and Entropy for Interpretable CNN Compression(KSE)

PyTorch implementation for KSE.


## Abstract

Compressing convolutional neural networks (CNNs) has received ever-increasing research focus. However, most existing CNN compression methods do not interpret their inherent structures to distinguish the implicit redundancy. In this paper, we investigate the problem of CNN compression from a novel interpretable perspective. The relationship between the input feature maps and 2D kernels is revealed in a theoretical framework, based on which a kernel sparsity and entropy (KSE) indicator is proposed to quantitate the feature map importance in a feature-agnostic manner to guide model compression. Kernel clustering is further conducted based on the KSE indicator to accomplish highprecision CNN compression. KSE is capable of simultaneously compressing each layer in an efficient way, which is significantly faster compared to previous data-driven feature map pruning methods. We comprehensively evaluate the compression and speedup of the proposed method on CIFAR-10, SVHN and ImageNet 2012. Our method demonstrates superior performance gains over previous ones. In particular, it achieves 4.7× FLOPs reduction and 2.9×compression on ResNet-50 with only a Top-5 accuracy drop of 0.35% on ImageNet 2012, which significantly outperforms state-of-the-art methods.


## Citation
If you find KSE useful in your research, please consider citing:

```
@inproceedings{li2018exploiting,
  title     = {Exploiting Kernel Sparsity and Entropy for Interpretable CNN Compression},
  author    = {Li, Yuchao and Lin, Shaohui and Zhang, Baochang and Liu, Jianzhuang and Doermann, David and Wu, Yongjian and Huang, Feiyue and Ji, Rongrong},
  booktitle = {Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
  year      = {2019}
}
```

## Running Code

In this code, you can run our Resnet-56 and Densenet-40 model on CIFAR10 dataset. The code has been tested by Python 3.5, [Pytorch 0.4.1](https://pytorch.org/) and CUDA 9.0 on Ubuntu 16.04.

## Running Example

### Train

#### CIFAR-10

##### ResNet-56 (G=4, T=0)

```shell
python train.py --net resnet56 --pretrained True --checkpoint pth/resnet56.pth --train_dir tmp/resnet56_G4T0 --train_batch_size 128 --learning_rate 0.01 --epochs 200 --schedule 100 --G 4 --T 0 
```

##### DensetNet-40 (G=5, T=0)

```shell
python train.py --net densenet40 --pretrained True --checkpoint pth/densenet40.pth --train_dir tmp/densenet40_G5T0 --train_batch_size 128 --learning_rate 0.01 --epochs 200 --schedule 100 --G 5 --T 0 
```

#### ImageNet

Modifying the 'train_image_dir' and 'val_image_dir' in dataset/imagenet.py to the path of ImageNet dataset,

##### ResNet-50 (G=5, T=1)

```shell
python train.py --net resnet50 --dataset imagenet --pretrained True --checkpoint resnet50.pth --train_dir tmp/resnet50_G5T1 --train_batch_size 64 --learning_rate 0.001 --epochs 21 --schedule 7 14 --G 5 --T 1 
```

##### Inception-v1 (G=4, T=1)

```shell
python train.py --net inception_v1 --dataset imagenet --pretrained True --checkpoint inception_v1.pth --train_dir tmp/inceptionv1_G4T1 --train_batch_size 64 --learning_rate 0.001 --epochs 21 --schedule 7 14 --G 4 --T 1 
```

### Test

##### ResNet-56 (G=4, T=0)

```shell
python test.py --net resnet56 --pretrained True --checkpoint tmp/resnet56_G4T0/model_best.pth --G 4 --T 0
```

##### DensetNet-40 (G=5, T=0)

```shell
python test.py --net densenet40 --pretrained True --checkpoint tmp/densenet40_G5T0/model_best.pth --G 5 --T 0
```

## Experiments

#### ResNet-50 (ImageNet2012)

| Model | Compression Ratio | Acceleration Ratio | Top-1 Acc. | Top-5 Acc. |  
| ------------- | ------------- | ------------- |  ------------- |   ------------- | 
| GDP-0.6 [1]| - | 2.2 | 71.89% | 90.71% | 
| ResNet-50(2×) [2] | - | 1.5 | 72.30% | 90.80% |
| ThiNet-50 [3] | 2.0 | 2.4 | 71.01% | 90.02% |
| KSE(G=5) | 2.6 | 3.8 | 75.51% | 92.69% |

#### Inception-v1 (ImageNet2012)

| Model | Compression Ratio | Acceleration Ratio | Top-1 Acc. | Top-5 Acc. |  
| ------------- | ------------- | ------------- |  ------------- |   ------------- | 
| Deep k-means [4] | 1.5 | - | 69.50% | 89.63% | 
| KSE(G=4)| 1.9 | 2.1 | 70.36% | 89.79% |

## References

[1] Shaohui Lin, Rongrong Ji, Yuchao Li, Yongjian Wu, Feiyue Huang, and Baochang Zhang. Accelerating convolutional networks via global & dynamic filter pruning. International Joint Conference on Artificial Intelligence (IJCAI), 2018.

[2] Yihui He, Xiangyu Zhang, and Jian Sun. Channel pruning for accelerating very deep neural networks. International Conference on Computer Vision (ICCV), 2017.

[3] Jian-Hao Luo, Jianxin Wu, and Weiyao Lin. Thinet: A filter level pruning method for deep neural network compression. International Conference on Computer Vision (ICCV), 2017.

[4] Wu J, Wang Y, Wu Z, et al. Deep k-Means: Re-Training and Parameter Sharing with Harder Cluster Assignments for Compressing Deep Convolutions. International Conference on Machine Learning (ICML), 2018.


## Tips

If you find any problems, please feel free to contact to the authors (xiamenlyc@gmail.com).
