# Educhat 学习记录

华东师范大学开发了 EduChat https://github.com/ECNU-ICALK/EduChat ， 现在应该也是在持续优化中。 作者极具共享精神，把很多模型、还有重要数据开源， 但文档写得有些不完整， 缺包、缺版本。 

经尝试， 目前可成功运行 sft-baichuan 模型。 可按以下步骤操作：

## 0. 下载模型的通用配置

直接使用镜像网站 https://hf-mirror.com/ 所提方法二：huggingface-cli


## 1. 环境配置

原文档少提及一些包, 为验证，我新建一个新环境验证。 本人使用的是 3090Ti 24G，需要 pytorch>=2.0 （4090肯定要）。 希望早日用上48G和80G的， 虽然说租几个小时肯定租得起。

```
conda create -n educhat python=3.9     # 创建conda 环境
conda activate educhat
pip install transformers==4.33.1 tokenizers==0.13.3 transformers_stream_generator==0.0.5 sentencepiece==0.2.0 accelerate==0.30.1
pip install jupyter notebook           # 可选
```

注： 
1. 需要安装pytorch或tf， 我使用的是 `pip install torch==2.3.0 torchvision==0.18.0`, 具体请查看 https://pytorch.org/get-started/locally/
2. transformers==4.41.x 运行 百川baichuan报错，'BaichuanTokenizer' object has no attribute 'sp_model'


## 2. 下载代码和模型

#### 非训练部分（截至 2024.06.01）

TryEduchat-baichuan.ipynb 文件 

### 模型下载 

#### 百川

https://huggingface.co/ecnu-icalk/educhat-sft-002-13b-baichuan

```
huggingface-cli download --resume-download ecnu-icalk/educhat-sft-002-13b-baichuan  --local-dir /path/to/educhat-sft-002-13b-baichuan
```
缺少 六分之五的模型参数文件， 需要从百度网盘上下载， 5个文件共计大概50G， 直接放到前面的文件夹中即可。

注：    
1. huggingface-cli 说是会在 $HOME/.cache/huggingface 创建符号链接， 我没太确认 是真符号链接还是什么， 因此我没有使用`ecnu-icalk/educhat-sft-002-13b-baichuan`， 而是使用绝对路径，见ipynb文件
2. 临时找个百度超级会员， 1、2块钱， 对我来说， 没必要单月40块、连续包月18。 具体店铺可见最后。

## 3. 运行

暂不涉及训练

### 百川

见 TryEduchat-baichuan.ipynb —— 暂不提供 Google Colab 链接， 因为模型参数文件大半在百度。
如果运行 qwen1.8B 成功，我再更新。

没有 half()  24G 显存爆掉， 但百川官方 https://huggingface.co/baichuan-inc/Baichuan-7B 所给代码 好像没有爆显存。

## Demo 运行

安装 

```
pip install mdtex2html==1.3.0 gradio==4.32.1
```

代码见 educhat_gradio.py， 大概有三处小改动。

```
python educhat_gradio.py --top_k 50 \
--do_sample True \
--max_new_tokens 512 \
--model_path /path/to/educhat_model 
```

注：  
1. 我这边会提示 frpc，这玩意儿是内网穿透（没有公网IP时让外网访问），  我不知道 gradio 居然有这个。
2. 速度不是很快， 我的才24G显存， 总提示  `Some parameters are on the meta device device because they were offloaded to the cpu.`

# Demo 效果

速度各不相同，不提了， 回答如图：

![educhat-demo](https://github.com/sndnyang/LearnIsFun/raw/master/images/educhat_demo.png)

评价： 挺死板的。

# TODO

- 跑通 qwen 1.8b 模型

- 转chat, 也就是像说话一样慢慢出字， 而不是全部完成后再显示

- 学习训练LLM， 使用所提供数据集进行训练

- 量化（学习）

- 接入 ollama

- 想想怎么评估


# 更新记录
- 20240601   
   **成功运行 educhat-sft-002-13b-baichuan**  
   **成功运行 gradio demo**
   花费 一天百度超级会员 2.65， 拼多多 晓黑板官方旗舰店， 下载 5个9G多文件
   qwen版 仍未通
- 202405  
   不成功的运行  
   尤其是 LLama版， 原始权重、解密初次听说， 暂无从下手， 输出代码——issue区 有人解码后也是乱码。
   