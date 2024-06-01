# Educhat 学习记录

华东师范大学开发了 EduChat https://github.com/ECNU-ICALK/EduChat ， 现在应该也是在持续优化中。 作者极具共享精神，把很多模型、还有重要数据开源， 但文档写得有些不完整， 缺包、缺版本。 

经尝试， 目前可成功运行 sft-baichuan 13B 和 qwen 1.8B 模型。 

## 0. 下载模型的通用配置

直接使用镜像网站 https://hf-mirror.com/ 所提方法二：huggingface-cli




# 使用训练好的模型

百川使用 `transformers==4.33.1 tokenizers==0.13.3`,  通义千问使用当前最新的`tokenizers-0.19.1 transformers-4.41.2`

百川使用 4.41.x 会报错， 通义千问使用 4.37以下会报错， 我不确定 4.37/4.38 是否通用——没测。


## 百川 baichuan 模型 13B

[https://github.com/sndnyang/LearnIsFun/blob/master/educhat/educhat-baichuan.md](https://github.com/sndnyang/LearnIsFun/blob/master/educhat/educhat-baichuan.md)

## 通义千问 Qwen 模型  1.8B

[https://github.com/sndnyang/LearnIsFun/blob/master/educhat/educhat-qwen.md](https://github.com/sndnyang/LearnIsFun/blob/master/educhat/educhat-qwen.md)


## LLama (待学习)

原始权重 处理， 新手没搞过， 加上应用优先用中文的~ 不一定会再试了。



# 训练

待学习



# TODO

- 转chat, 也就是像说话一样慢慢出字， 而不是全部完成后再显示

- 学习训练LLM， 使用所提供数据集进行训练

- 量化（学习）

- 接入 ollama

- 想想怎么评估


# 更新记录
- 20240601   
   **成功运行 educhat-sft-002-13b-baichuan**    
   **成功运行 gradio demo**   
   **晚上成功运行 qwen 1.8B 模型**    
   花费 一天百度超级会员 2.65， 拼多多 晓黑板官方旗舰店， 下载 5个9G多文件  
- 202405  
   不成功的运行  
   尤其是 LLama版， 原始权重、解密初次听说， 暂无从下手， 输出代码——issue区 有人解码后也是乱码。
   