# google cloud云端0成本部署comfyUI体验SDXL模型
你还需要花钱购买midjourney会员来享用AI作图工具吗，答案肯定是否定的，看完后你就知道怎么实现了，如果觉得满意的话请给个star哦。

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


中文版内容资料陆续更新中，包括nodes各个节点和参数的应用以及说明(包括controlnet插件，LoRA'S，upscaling,inpaint and outpaint等等)，敬请期待

