# Educhat-Qwen 学习记录

经尝试， 目前可成功运行 sft-13b-baichuan 模型。 可按以下步骤操作：

## 1. 环境配置

原文档少提及一些包, 为验证，我新建一个新环境验证。 本人使用的是 3090Ti 24G，需要 pytorch>=2.0 （4090肯定要）。 希望早日用上48G和80G的， 虽然说租几个小时肯定租得起。

```
conda create -n educhat python=3.9     # 创建conda 环境
conda activate educhat
pip install transformers==4.41.2 tokenizers==0.19.1 transformers_stream_generator==0.0.5 sentencepiece==0.2.0 accelerate==0.30.1
pip install jupyter notebook           # 可选
# pip install flash-attn --no-build-isolation   #  我这边安装使用
```

注： 
1. 需要安装pytorch或tf， 我使用的是 `pip install torch==2.3.0 torchvision==0.18.0`, 具体和cuda配套请查看 https://pytorch.org/get-started/locally/
2. 官方说 transformers>=4.37.0 , 否则会报错 KeyError: 'qwen2'


## 2. 下载代码和模型


### 模型下载 

可以直接看 TranEduchat-qwen.ipynb, 直接在colab上测试通过， 本地应该也通过了。

下载地址 https://huggingface.co/ecnu-icalk/educhat-sft-002-1.8b-qwen1.5/tree/main

```
huggingface-cli download --resume-download  ecnu-icalk/educhat-sft-002-1.8b-qwen1.5  --local-dir /path/to/educhat-sft-1.8b-qwen1.5
```

缺少两个文件 merges.txt (也可能只缺少这一个)，  以及 tokenizer.json, 去通义千问官方 https://huggingface.co/Qwen/Qwen1.5-1.8B-Chat/tree/main

没有文件，在运行时会报错， 错误大概就是 merges文件为空（没找到）， 经对比 两个模型文件差异， 我把两个文件都补上了。


注：    
1. huggingface-cli 说是会在 $HOME/.cache/huggingface 创建符号链接， 我还是没太确认 是真符号链接还是什么， 因此我没有调用`ecnu-icalk/educhat-sft-002-1.8b-qwen1.5`， 而是使用绝对路径，见ipynb文件


## 3. 运行


见 TryEduchat-qwen.ipynb


## Demo 运行（待定）

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


