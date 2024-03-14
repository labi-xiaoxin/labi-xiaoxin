# AMD芯片使用Stable-Diffusion

由于A卡的Stable Diffusion工具的逐步完善，之前只能使用CPU跑，现在已支持AMD显卡进行AI绘图。

## 下载

> 官网链接：[https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Install-and-Run-on-AMD-GPUs](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Install-and-Run-on-AMD-GPUs)
>
>按官方教程，我安装有异常情况，这里推荐使用：B站[秋葉aaaki](https://space.bilibili.com/12566101)的[【AI绘画】Stable Diffusion A卡专用整合包（DirectML）](https://www.bilibili.com/read/cv26557731/)

下载链接：
- 百度网盘：https://pan.baidu.com/s/1QDqo2uEoUS_NY1olb4vmVQ?pwd=aaki
- 夸克网盘：https://pan.quark.cn/s/19a36cab36ac
- 防止过期，我的夸克网盘：https://pan.quark.cn/s/b169f98f32b4
- sha1校验码：c7c5d497360c7ec3fe9af5ada1624842341d8275

下载完成并解压后，目录如图：
![解压目录](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141327668.png)


## 启动器

在目录下，找到`A启动器.exe`，双击执行它。
在第一次启动时，这里会自动加载一些依赖项，耐心等待即可。。。
![启动应用程序](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141332947.png)

启动完成后，会进入主界面：
![启动器主界面](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141334710.png)

至此，启动器启动成功

## 修改生成引擎
`高级选项`——`性能设置`——`生成引擎`——选择`DML XX `
![修改生成引擎](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141348263.png)


## 导入模型

有许多网站有各种大神分享的模型效果，我们看到适合的模型下载后即可导入模型。

>[Hugging Face](https://huggingface.co/)
>[C站](https://civitai.com/)

- 进入`模型管理`页面
![模型管理](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141338514.png)
- 可以直接下载`模型管理`内的模型，也可以导入其他网站下载的模型
- 点击`添加模型`
![添加模型](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141339293.png)
![找到模型，并打开](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141340383.png)

## 一键启动

- 进入`一键启动`页面，点击`一键启动`
![一键启动](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141341159.png)
- 启动后，会进入命令行，执行相应代码，安装所需依赖，如有任何问题在命令行里可以查看
![安装所需依赖](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141343119.png)
- 启动成功后，会看到这么一串地址
![启动成功](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141344517.png)
- 复制地址，进入浏览器
![进入界面](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141346892.png)

至此，Stable Diffusion启动成功

## 开始AI绘图

输入正向提示词:
```prompt
masterpiece,illustration,best_quality,rosaria_\(genshin_impact\),<lora:rosaria_anything_v4:0.95>,nun,fishnet,shoulder_gloves,
bare_shoulder,bangs,(pray:1.2),hands together,sitting on floor,church,looking up,crying with eyes open,looking up,
<lora:Moxin_10:0.2>,<lora:LORAChineseDoll_chinesedolllikeness1:0.2>,<lora:tifaMeenow_tifaV2:0.5>,red hair,red eyes,headdress,
short hair,skinny,crown,
[after]{zoom_enhance mask="fingers" replacement="closeup hand" max_denoising_strength=0.2 precision=80}[/after],white gloves,
```

输入反向提示词:
```prompt
wrinkles Deformed eyes,((disfigured)),((bad art)),((deformed)),((extra limbs)),(((duplicated))),((morbid)),((mutilated)),
out of frame,extra fingers,mutated hands,poorly drawn eyes,((poorly drawn hands)),((poorly drawn face)),(((extra legs))),
(fused fingers),(too many fingers),(((long neck))),tiling,poorly drawn,mutated,cross-eye,canvas frame,frame,cartoon,3d,
weird colors,blurry,((old)),((ugly)),((child)),NG_DeepNegative_V1_75T,(extra hand:1.4),
```

点击`生成`，则使用显卡进行绘图，这里可以看看显卡是否在运行

![绘图中](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141355093.png)

![绘图完成](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202403141356382.png)

至此，恭喜你get`Stable Diffusion`初步使用。
