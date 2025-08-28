# GPT-SoVITS
使用GPT-SoVITS人声模型训练

·技术原理：GPT-SoVITS通过整合VITS（变分自编码器+流模型）与VALLE（语音量化自回归模型），实现了声纹克隆的两大突破：

语音离散化编码：采用HuBERT模型对语音进行掩码预测，在保留内容信息的同时剥离部分音色特征，通过自回归机制将参考语音的音色“泄漏”至目标语音，增强音色迁移效果。

长文本声纹提取：引入MRTE（Megatts2技术），通过注意力机制捕捉长句中的声纹特征，解决传统模型在长语音合成中的音色失真问题。


·操作步骤：
1.采集声源片段大约10min到2h

2.处理生源片段的杂音

（使用urv5分离伴奏，消除混响和声，保留呼吸声等自然特征）

<img width="400" height="500" alt="图片2" src="https://github.com/user-attachments/assets/fe7109e1-f1ab-485a-8e06-77dc881b324f" />
<img width="400" height="500" alt="图片3" src="https://github.com/user-attachments/assets/b3a0b205-9fd1-4203-871f-1dbecd833f79" />


3.使用Audio-Slicer-GUI对音频切段（按静音段分割音频生成5-10秒短句）

<img width="600" height="400" alt="图片1" src="https://github.com/user-attachments/assets/e1286900-6130-478e-9ee3-3ad67049d97d" />


4.数据预处理

（将原始数据转化为适合机器学习模型的高质量数据集，从而提升模型训练的效率、稳定性和最终性能。）

5.写入配置文件

from omegaconf import OmegaConf

cfg = OmegaConf.create({

    "model": {
    
        "type": "DiffSinger",
        
        "vocoder": "nsf-hifigan",
        
        "audio": {
        
            "sample_rate": 44100,
            
            "hop_length": 512
            
        }
        
    }
    
})

OmegaConf.save(cfg, "model_config.yaml")


6.预训练+微调

训练是指使用目标说话人的音声数据集令 AI 学习特征并生成神经网络模型。

 1.学会通用语音规律，让模型听懂“人怎么说话”，包括语调、节奏、发音方式等。
 
 2.减少你后期训练的数据量

 
7.推理

训练是让模型“学会说话”，推理是让模型“开口说话”，接下来就可以使用该模型实现文字转语音、语音转语音、实时/离线生成等功能

GPT-SoVITS整合包：

链接：https://pan.baidu.com/s/1QpadHsp7fQbQLFtSV6G9lg 

提取码：6369 

（感谢bilibili@羽毛布団、bilibili@花儿不哭大佬们的分享和教学）

