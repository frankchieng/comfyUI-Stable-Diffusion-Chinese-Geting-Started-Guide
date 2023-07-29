# google cloud云端0成本部署comfyUI体验SDXL模型
你还需要花钱购买midjourney会员来享用AI作图工具吗，答案肯定是否定的，看完后你就知道怎么实现了，如果觉得满意的话请给个star哦。

# comfyUI和sdxl1.0 colab运行
SDXL1.0正式版上线后，不需要再下载base model和refine model的模型，直接挂载huggingface上面的safetensor文件到comfyUI目录下面的/models/checkpoints/路径即可：

```
!wget -c https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0/resolve/main/sd_xl_base_1.0.safetensors -P ./models/checkpoints/
```
```
!wget -c https://huggingface.co/stabilityai/stable-diffusion-xl-refiner-1.0/resolve/main/sd_xl_refiner_1.0.safetensors -P ./models/checkpoints/
```
VAE同样：
```
!wget -c https://huggingface.co/stabilityai/sdxl-vae/resolve/main/sdxl_vae.safetensors -P ./models/vae/
```

# comfyUI和sdxl0.9模型下载和上传云空间
comfyUI采用的是workflow体系来运行Stable Diffusion的各种模型和参数，有点类似于桌面软件widgets,各个控制流节点可以拖拽，复制，resize改变大小等，更方便对最终output输出图片的细节调优。

最新的sdxl破解版model分别为sd_xl_base_0.9.safetensors和sd_xl_refiner_0.9.safetensors，普通无压缩下载12.9GB和5.65GB，太大了，再加上comfyUI的下载版ComfyUI_windows_portable_nvidia_cu118_or_cpu.7z也有差不多1.43GB，

[点此下载](https://github.com/comfyanonymous/ComfyUI/releases/download/latest/ComfyUI_windows_portable_nvidia_cu118_or_cpu.7z)支持Nvidia GPU版本comfyUI压缩包：

下面的链接是sdxl的pruned版的下载，总共差不多12.12GB 

https://drive.google.com/drive/folders/1JVNLya7JsiUqR7l8I6avk1pmkEXFm32O

https://mega.nz/folder/QSVFiBrS#Nq2BWbG-0bsdWoyd3AhdZw

因为不是local跑模型，国内的比如autoDL的GPU3060RTX，4080RTX等都是按小时，天或者月收费，因此选择了目前性价比最高的google colab来跑comfyUI,colab提供了一定额度和时间的免费NVIDIA tesla T4 GPU，为了便于每次访问不需要再重新上传一遍文件，需要配合把上面提到的安装包上传到google driver也就是谷歌云盘上，这样每次colab运行的时候只需要mount加载google driver的文件内容即可，不过这么大的文件上传到google drive速度是很慢的，而国内一般普通会员的云盘上传最多只提供5G的免费容量，为了增加文件上传大小和速度，选择了MASV - Fast, Large File Transfer Service，链接如下：

https://massive.io/send-large-files/ 

大文件传输速度网速可以的话基本都在1Mbps以上，可以直接google账号免注册登录，每个账号提供20G的免费空间。文件传完后，可以在Cloud Intergration菜单下面加载google drive,把上传的文件transfer过去就可以，速度非常快。
![image](https://github.com/frankchieng/comfyUI-SDXL-Chinese-Geting-Started-Guide/blob/main/assets/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20230710230548.png)

# google colab安装comfyUI和sdxl 0.9版本的base model,refiner model
你可以在google colab上运行此[python脚本](https://github.com/frankchieng/comfyUI-SDXL-Chinese-Geting-Started-Guide/blob/main/comfyui_colab.ipynb)(解压comfyUI后把sd_xl_base_0.9.safetensors和sd_xl_refiner_0.9.safetensors放在ComfyUI\models\checkpoints),访问如下图的链接并填写IP地址后出现comfyUI运行页面代表启动成功。

![image](https://github.com/frankchieng/comfyUI-SDXL-Chinese-Geting-Started-Guide/blob/main/assets/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20230711011657.png)

![image](https://github.com/frankchieng/comfyUI-SDXL-Chinese-Geting-Started-Guide/blob/main/assets/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20230711011739.png)

finally，我们终于成功运行起了comfyUI的用户界面

![image](https://github.com/frankchieng/comfyUI-SDXL-Chinese-Geting-Started-Guide/blob/main/assets/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20230711013035.png)

下载此[workflow的json文件](https://github.com/frankchieng/comfyUI-SDXL-Chinese-Geting-Started-Guide/blob/main/Workflow%20ComfyUI%20SDXL%200.9.json)并把他Load加载到comfyUI里，即可以开始你的sdxl模型的comfyUI作图之旅了。

![image](https://github.com/frankchieng/comfyUI-SDXL-Chinese-Geting-Started-Guide/blob/main/assets/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20230711013918.png)

如下图refiner model生成的图片质量和细节捕捉要好过base model生成的图片，没有对比就没有伤害！

base model image:

![image](https://github.com/frankchieng/comfyUI-SDXL-Chinese-Geting-Started-Guide/blob/main/assets/base_output_00003_.png)

refiner model image:

![image](https://github.com/frankchieng/comfyUI-SDXL-Chinese-Geting-Started-Guide/blob/main/assets/refiner_output_00001_.png)

如果你升级google colab为Pro或者Pro+会员，GPU可以选择更强大的Nvidia的A100和V100 GPU，1块A100的训练速度是1一块V100的3.4倍； 使用混合精度时，前者则是后者的2.6倍。 其中，分别用8块A100与8块V100，进行32位训练：前者速度能够达到后者的3.5倍。一个月可以有100个计算单元computer units可用。[点击此处](https://github.com/frankchieng/comfyUI-Stable-Diffusion-Chinese-Geting-Started-Guide/blob/main/Making_the_Most_of_your_Colab_Subscription.ipynb)查看GPU运行时信息以及是否使用了high-RAM，以便切换更高的运行时内存。

中文版内容资料陆续更新中，包括nodes各个节点和参数的应用以及说明(包括controlnet插件，LoRA'S，upscaling,inpaint and outpaint等等)，敬请期待

除了用comfyUI的workflow添加nodes节点形式来运行SDXL1.0模型之外，如果需要训练LoRA,controlnet等，建议使用diffusers pipeline，能调整更多的参数
LoRA和controlnet对于GPU配置要求比较高，建议40G VRAM的A100 GPU来训练，比较耗显存

什么是pipeline?
pipeline管道是一个端到端的类能够提供快速和简便的方法来使用diffusion系统，为了能够独立的捆绑训练好的模型和scheduler调度器来进行推理.一些特定的模型和调度器的组合定义了特殊的pipeline管道类型，比如StableDiffusionPipeline或StableDiffusionControlNetPipeline。所有的pipeline类型继承自基础DiffusionPipeline类。传递任意的checkpoint，它会自动的检测pipeline管道类型并且加载必须的组件。

目前的SDXL1.0模型pipeline主要有三个，第一个是Text-to-Image的StableDiffusionXLPipeline，调用stable-diffusion-xl-base-1.0的base模型。第二个是
Image-to-image的StableDiffusionXLImg2ImgPipeline，调用stable-diffusion-xl-refiner-1.0的refiner模型。第三个是Inpainting的StableDiffusionXLInpaintPipeline。

SDXL有一个特别有意思的地方：能够传递多个不同的prompts至每个text-encoder,也就是组合prompts能生成非常有想象力的图片。

Stable Diffusion XL 是在两个text encoders文本编码器上面做的训练。默认的行为是传递同样的prompt到每一个text encoders里。但也能够传递不同的prompt到每一个text-encoder,一些用户发现这样做能够提高图片质量。为了实现这个效果, 除了prompt和negative_prompt之外你还能够传递prompt_2和negative_prompt_2 。原始的prompt和negative prompt传递至text_encoder (官方 SDXL 0.9/1.0用的文本编码器是OpenAI CLIP-ViT/L-14), 而prompt_2和negative_prompt_2传递至text_encoder_2 (官方SDXL 0.9/1.0的文本编码器是OpenCLIP-ViT/bigG-14)。

比如下面的prompt提示词分别为

prompt = "award winning photograph of elephant"

prompt_2 = "award winning photograph of octopus"

组合后能生成出来既像大象又像章鱼的奇怪生物

另外由于sdxl1.0生成图片非常消耗GPU的显存，每次生成图片之前最好加上pipe.vae.enable_tiling()和pipe.enable_model_cpu_offload()以便于避免出现cuda out of memory显存不够用而导致运行崩溃的错误

![image](https://github.com/frankchieng/comfyUI-Stable-Diffusion-Chinese-Geting-Started-Guide/blob/main/assets/diffusers.png)

![image](https://github.com/frankchieng/comfyUI-Stable-Diffusion-Chinese-Geting-Started-Guide/blob/main/assets/elephant_octopus1.png)

点击获取[comfyUI和diffusers的colab部署代码](https://colab.research.google.com/drive/1yO30qPLybCj8OatCUxloC6G5j9VrXdFF?usp=sharing)

[ComfyUI使用的案例](https://github.com/frankchieng/comfyUI-Stable-Diffusion-Chinese-Geting-Started-Guide/blob/main/ComfyUI_examples/README.md)

交流进微信群可以扫码添加此微信：

![image](https://github.com/frankchieng/imagegeneration/blob/main/wechat.jpg)

