所有代码库里的图片包括了元数据，意味着它们能通过Load按钮加载进ComfyUI(或者拖拽图片进入comfyUI窗口)来获得整个workflow生成图片
1.文字生成图片后的画质提升 ComfyUI/models/upscale_models文件夹下面加载如下文件

[1x Skin Detailer Upscaler (load pth and yaml into same folder)](https://drive.google.com/drive/folders/1VkT6tpbCPn2gKZYPtawDJGMpLg6EyRpO)

[4x NMKD Upscaler](https://huggingface.co/gemasai/4x_NMKD-Siax_200k/tree/main)

[4x Ultrasharp Upscaler](https://mega.nz/folder/qZRBmaIY#nIG8KyWFcGNTuMX_XNbJ_g)

[workflow的加载json文件](https://github.com/frankchieng/comfyUI-Stable-Diffusion-Chinese-Geting-Started-Guide/blob/main/ComfyUI_examples/assets/upscale_model.json)

refined model出图：

![image](https://github.com/frankchieng/comfyUI-Stable-Diffusion-Chinese-Geting-Started-Guide/blob/main/ComfyUI_examples/assets/SDXL_0.9_Output_00001_.png)

4x Ultrasharp Upscaler出图，明显能看到分辨率更高，而且人的皮肤等细节处理的更光滑，更清晰：
![image](https://github.com/frankchieng/comfyUI-Stable-Diffusion-Chinese-Geting-Started-Guide/blob/main/ComfyUI_examples/assets/UpScaled_Upscaled_SDXL09__00002_.png)

[点击此处](https://github.com/frankchieng/comfyUI-Stable-Diffusion-Chinese-Geting-Started-Guide/blob/main/ComfyUI_examples/Sytan%20SDXL%20Workflow%20v0.5.json)获取目前我个人感觉最好的实物摄影风格和景深的workflow代码

说明：
Prompting: linguistic prompt语义提示框, 用语法正确的一句话的自然语言来描述图片。例如:A photograph of a (subject主语) in a (location地点) at (time时间)，这样更符合大部分用户的语言习惯一气呵成的句子。然后第二个文本框选择一些精挑细选的标签来增强prompt效果, 比如:cinematic影院级效果, bokeh散景, photograph照片级, (features about subject是关于主语的特征) Full prompt example: Linguistic: A cinematic photograph of a pretty woman with blonde hair and blue eyes in a park at sunset.Supporting: clouds, nature, bokeh, f1.8, cinematic lighting, entered composition Photographic tips照片级别画质技巧1. Try and use words or entities that tie into realistic imagery, such as National geographic, Vogue, ethnographic, portrait, and similar words 2. Do not use words 不要用下列词汇like "realism" or "realistic" when prompting for photographs, as they are associated with art styles that depict "realistic" things, and such will weight towards traditional or digital art 3. Feel free to use compositional words可以自由的使用组合词组, such as "centered subject" or "(object) to the side", this can help a lot for achieving different and interesting results 4. I recommend not going over 6 on the positive aesthetic score for the refiner when going for realism, I find that the higher you go, the more your images are likely to go into the direction of aesthetic paintings

这第四点是什么意思呢？什么是aesthetic score?
模型所有的图片在预训练的阶段有他们自己的aesthetic score,姑且叫做美学评分，0是最丑的, 10是最好看的，正面词设置的时候不要把这个值设置超过6因为图片会开始被过分处理变得很假。

上述例子生成图![image](https://github.com/frankchieng/comfyUI-Stable-Diffusion-Chinese-Geting-Started-Guide/blob/main/ComfyUI_examples/assets/ComfyUI_00001_.png)
