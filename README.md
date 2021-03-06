# 基于tensorflow的语音识别系统
## 简介
基于 tensorflow 的中文语音识别框架, 模型结构参考 百度[Deepspeech2](http://proceedings.mlr.press/v48/amodei16.pdf) 的论文,训练语料采用Aishell 170 小时数据. 模型结构如下图所示:

<p align="center">
<img src="img/arc.png">
<br/> 百度Deepspeech2 语音识别模型结构
</p>

**目前模型训练存在不收敛情况，正在调参研究中**

## 安装
### Prerequisites
* 本程序基于 Python2.7    
* Tensorflow 版本应大于1.3，否则tf.nn.softmax等函数可能报错

### Setup

* 安装以下依赖库 pkg-config, flac, ogg, vorbis, boost and swig,在Ubuntu 环境下可以通过apt-get 进行安装
'''
sudo apt-get install -y pkg-config libflac-dev libogg-dev libvorbis-dev libboost-dev swig
'''

## 运行

* 进入conf文件夹,修改 hyparam.py 中的模型参数 
* 进入example/aishell 修改 run_data.sh 内相关存储路径后，运行该脚本生成 manfest.{train,dev,test} 文件、vocab.txt以及 mean_std.npz
* 运行 train.py 训练模型    
* 运行test.py 进行测试

## server/client 运行

* 打开 ./demo_client.sh or ./demo_server.sh 文件配置 IP、端口等信息
* 执行 ./demo_server.sh 启动服务器    
* 执行 ./demo_client.sh 启动客户端   
* 在客户端内，持续按空格进行录音，松开空格后发送音频到服务器端进行语音识别

## 语言模型
语言模型采用的是百度提供的中文语言模型，由KenLM工具生成并剪枝得到。详情请查看[Mandarin LM](https://github.com/PaddlePaddle/DeepSpeech#mandarin-lm)

### 语言模型参数
语言模型用于测试和使用阶段的解码。因此当声学模型训练时，语言模型的参数也需要进行改变。hyparam里的参数只是随手写的...

## TODO
* 对模型进行调参或结构调整使其能够使用。

## Ref
以 [xxbb1234021/speech_recognition](https://github.com/xxbb1234021/speech_recognition) 和 [PaddlePaddle/Deepspeech2](https://github.com/PaddlePaddle/DeepSpeech)为基础进行修改
