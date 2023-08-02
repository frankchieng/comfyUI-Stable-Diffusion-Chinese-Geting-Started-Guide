# SDXL1.0引擎LoRA训练

运行环境：google colab
运行配置minimum要求:Tesla T4 16GB RAM，CPU VRAM25GB

你可以直接点击下面图标运行sdxl的LoRA模型，纯python编程跑模型，比传统的webUI和workflow能配置更多的参数和超参数
[![](https://img.shields.io/static/v1?message=Open%20in%20Colab&logo=googlecolab&labelColor=5c5c5c&color=0f80c1&label=%20&style=flat)](https://colab.research.google.com/drive/1jLdpH8rkrLUbSmvc-3-ZMSyK6KTsejaB?usp=sharing) 

图片预训练和处理用到了：Image Browser;Imageboard Scraper和discordia-archivum，discordia-archivum能够让你通过在discord上抓取bot和channel下面的图片以及附件。

训练图片自动打标签和标题用到了:BLIP Captioning和动漫风格的Waifu Diffusion 1.4 Tagger V2

因为stable diffusion的处理机制以comfyUI的workflow举例，先通过prompt然后Clip text encoder,先生成的是latent images，经过sampler以及VAE最后才能生成pixel image,
所以我们需要中间加一步Bucketing and Latents Caching潜藏图片的缓存步骤

图片pre-training之后就要开始训练数据了

重点参数配置说明:
神经网络采用LoRA-C3Lier，除了Linear Layer线性层network_dim训练外，还可以用Convolutional Layer卷积层的conv_dim来训练，convolutional kernel应该是3x3
optimizer_type优化器选择了Adafactor，之前无论用diffusers跑的时候选择的AdamW 8bit在torch2.x以及xformer2.0.0依赖下面，经常会出现CUDA out of memory的报错，
GPU的RAM要求比较高，learning_rate学习率设置为1e-5，为了节省显存，num_repeats设为1，epochs设为10，每跑一次epoch,出来一个lora的safetensors节点和一张该节点的
训练后式例图片，mixed_precision混合精读设为fp16,sample采样器选择euler_a

所有参数配置文件在sdxl_lora/config_file.toml和sdxl_lora/sample_prompt.toml，可以下载后自行参考修改

anime动漫风格训练图片已上传至[huggingface datasets](https://huggingface.co/datasets/frank-chieng/hitokomoru-lora-sdxl1.0base)

LoRA训练10次epochs的safetensors已经训练结束后最终的模型在[huggingface models](https://huggingface.co/frank-chieng/hitokomoru/tree/main/output)

最后inference推理通过prompt: 1girl, aqua eyes, baseball cap, blonde hair, closed mouth, earrings, green background, hat, hoop earrings, jewelry, looking at viewer, shirt, short hair, simple background, solo, upper body, yellow shirt
生成的训练后图片
![image](https://github.com/frankchieng/comfyUI-Stable-Diffusion-Chinese-Geting-Started-Guide/blob/main/assets/sdxl_lora_20230801152910_e000003_00.png)
