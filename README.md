# A Deep-Learning-Based Chinese Speech Recognition System
基于深度学习的中文语音识别系统，如果您觉得喜欢，请点一个 **"Star"** 吧~

[![GPL-3.0 Licensed](https://img.shields.io/badge/License-GPL3.0-blue.svg?style=flat)](https://opensource.org/licenses/GPL-3.0) [![TensorFlow Version](https://img.shields.io/badge/Tensorflow-1.4+-blue.svg)](https://www.tensorflow.org/) [![Keras Version](https://img.shields.io/badge/Keras-2.0+-blue.svg)](https://keras.io/) [![Python Version](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/) 

**ReadMe Language** | 中文版 | [English](https://github.com/nl8590687/ASRT_SpeechRecognition/blob/master/README_EN.md) |

[查看本项目的Wiki页面](https://github.com/nl8590687/ASRT_SpeechRecognition/wiki) 

如果程序运行期间或使用中有什么问题，可以及时在issue中提出来，我将尽快做出答复。本项目作者交流QQ群：**867888133**

提问前可以先 [查看常见问题](https://github.com/nl8590687/ASRT_SpeechRecognition/wiki/issues) 避免重复提问

ASRT的原理请查看本文：
* [ASRT：一个中文语音识别系统](https://blog.ailemon.me/2018/08/29/asrt-a-chinese-speech-recognition-system/)

关于经常被问到的统计语言模型原理的问题，请看：

* [统计语言模型：从中文拼音到文本](https://blog.ailemon.me/2017/04/27/statistical-language-model-chinese-pinyin-to-words/)
* [无需中文分词算法的简单词频统计](https://blog.ailemon.me/2017/02/20/simple-words-frequency-statistic-without-segmentation-algorithm/)

## Introduction 简介

本项目使用Keras、TensorFlow基于深度卷积神经网络和长短时记忆神经网络、注意力机制以及CTC实现。

This project uses Keras, TensorFlow based on deep convolutional neural network and long-short memory neural network, attention mechanism and CTC to implement.

* **操作步骤**

首先通过Git将本项目克隆到您的计算机上，然后下载本项目训练所需要的数据集，下载链接详见[文档末尾部分](https://github.com/nl8590687/ASRT_SpeechRecognition#data-sets-%E6%95%B0%E6%8D%AE%E9%9B%86)。
```shell
$ git clone https://github.com/nl8590687/ASRT_SpeechRecognition.git
```

或者您也可以通过 "Fork" 按钮，将本项目Copy一份副本，然后通过您自己的SSH密钥克隆到本地。

通过git克隆仓库以后，进入项目根目录；并创建子目录 `dataset/` (可使用软链接代替)，然后将下载好的数据集直接解压进去
```shell
$ cd ASRT_SpeechRecognition

$ mkdir dataset

$ tar zxf <数据集压缩文件名> -C dataset/ 
```

然后需要将datalist目录下的文件全部拷贝到 `dataset/` 目录下，也就是将其跟数据集放在一起。
```shell
$ cp -rf datalist/* dataset/
```

目前可用的模型有24、25和251

运行本项目之前，请安装必要的[Python3版依赖库](https://github.com/nl8590687/ASRT_SpeechRecognition#python-import)

本项目开始训练请执行：
```shell
$ python3 train_mspeech.py
```
本项目开始测试请执行：
```shell
$ python3 test_mspeech.py
```
测试之前，请确保代码中填写的模型文件路径存在。

ASRT API服务器启动请执行：
```shell
$ python3 asrserver.py
```

如果要训练和使用模型251，请在代码中 `import SpeechModel` 的相应位置做修改。

* **errors in trianing**
1_error.I tensorflow/core/platform/cpu_feature_guard.cc:140] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
1_solve.在开头加上这两行可以解决
  import os
  os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'


## Model 模型

### Speech Model 语音模型

CNN + LSTM/GRU + CTC

* 关于下载已经训练好的模型的问题

可以在Github本仓库下[releases](https://github.com/nl8590687/ASRT_SpeechRecognition/releases)里面的查看发布的各个版本软件的压缩包里获得完整源程序。

### Language Model 语言模型

基于概率图的最大熵隐马尔可夫模型

## About Accuracy 关于准确率

当前，最好的模型在测试集上基本能达到80%的汉语拼音正确率

不过由于目前国际和国内的部分团队能做到97%，所以正确率仍有待于进一步提高

* 目前可知的可以继续提高准确率的一个方案就是纠正数据集标注错误，尤其是ST-CMDS里面关于syllable文件中拼音的错误，这里面有一定比例的错误标注，如果走过路过的各位有意愿尽自己的能力帮助纠正一些数据标注错误的，我将非常欢迎，可以通过提交Pull Request来纠正，并且将登上本仓库的贡献者名单。

样例：`不是： bu4 shi4 -> bu2 shi4` `一个：yi1 ge4 -> yi2 ge4` `了解：le5 jie3 -> liao3 jie3`

* 已订正部分：

ST-CMDS

train:  20170001P00001A    20170001P00001I    20170001P00002A

## Python Import
Python的依赖库

* python_speech_features
* TensorFlow
* Keras
* Numpy
* wave
* matplotlib
* math
* Scipy
* h5py

## Data Sets 数据集
* **清华大学THCHS30中文语音数据集**

data_thchs30.tgz 

[OpenSLR国内镜像](<http://cn-mirror.openslr.org/resources/18/data_thchs30.tgz>)
[OpenSLR国外镜像](<http://www.openslr.org/resources/18/data_thchs30.tgz>)

test-noise.tgz 

[OpenSLR国内镜像](<http://cn-mirror.openslr.org/resources/18/test-noise.tgz>)
[OpenSLR国外镜像](<http://www.openslr.org/resources/18/test-noise.tgz>)

resource.tgz 

[OpenSLR国内镜像](<http://cn-mirror.openslr.org/resources/18/resource.tgz>)
[OpenSLR国外镜像](<http://www.openslr.org/resources/18/resource.tgz>)

* **Free ST Chinese Mandarin Corpus** 

ST-CMDS-20170001_1-OS.tar.gz 

[OpenSLR国内镜像](<http://cn-mirror.openslr.org/resources/38/ST-CMDS-20170001_1-OS.tar.gz>)
[OpenSLR国外镜像](<http://www.openslr.org/resources/38/ST-CMDS-20170001_1-OS.tar.gz>)

* **AIShell 开源版数据集** (本项目暂未使用，之后会加入)

data_aishell.tgz

[OpenSLR国内镜像](<http://cn-mirror.openslr.org/resources/33/data_aishell.tgz>)
[OpenSLR国外镜像](<http://www.openslr.org/resources/33/data_aishell.tgz>)

* **Primewords Chinese Corpus Set 1** (本项目暂未使用，之后会加入)

[OpenSLR国内镜像](<http://cn-mirror.openslr.org/resources/47/primewords_md_2018_set1.tar.gz>)
[OpenSLR国外镜像](<http://www.openslr.org/resources/47/primewords_md_2018_set1.tar.gz>)

特别鸣谢！感谢前辈们的公开语音数据集

如果提供的数据集链接无法打开和下载，请点击该链接 [OpenSLR](http://www.openslr.org)

## Log
日志链接：[进展日志](https://github.com/nl8590687/ASRT_SpeechRecognition/blob/master/log.md)

## Contributors 贡献者们
@ZJUGuoShuai @williamchenwl

@nl8590687 (repo owner)

[**打赏作者**](https://github.com/nl8590687/ASRT_SpeechRecognition/wiki/donate)
