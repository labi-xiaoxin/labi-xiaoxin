>前端基于开源项目：wechaty实现微信网页版功能，感兴趣的小伙伴可以自行研究。
>前端代码已开源：https://github.com/labi-xiaoxin/wechat-bot-wechat4u.git

本项目搭建愿景：

1、在无法科学上网的情况下，实现ChatGPT对话。

2、提供社群消息处理、构建私域管理。

-----

**<center>一、功能介绍</center>**

 - `消息自动回复`：支持前端处理，支持对接后端接口实现更多功能
 - `群聊白名单`：支持指定名单内群聊回复
 - `私聊白名单`：支持指定名单内私聊回复
 - 支持`手机同时在线`：基于网页版API开发，能够在手机登录微信时，同时使用机器人
 - `接入ChatGPT`：理论上4也能支持，图片暂不支持。

----

**<center>二、搭建私人ChatGPT机器人说明</center>**


>技术教程：https://github.com/labi-xiaoxin/wechat-bot-wechat4u.git
>
>需要自行搭建后端，也可使用本人提供的后端（后台联系）
>
>现支持直接请求ChatGPT，无需另外搭建后端

 - 本地需要NodeJS环境，版本推荐18.0.0以上
 	- 官方下载地址：https://nodejs.org/download/release/v18.0.0/
- 下载代码
    - Github:https://github.com/labi-xiaoxin/wechat-bot-wechat4u.git
	- 无法访问Github，网盘下载：链接: https://pan.baidu.com/s/1fhYZY-jOs0_4ifiKpx4w6w?pwd=5xsc 提取码: 5xsc
- 进入项目目录，执行`npm install`，下载依赖
-  修改相关参数：
	- **config.js**：

		- `robotName`：机器人名，自定义你的机器人名字

		- `roomWhiteList`：群聊白名单，群聊的名字，只有在名单内才回复

		- `aliasWhiteList`：联系人白名单，私聊的备注，只有在名单内才回复

		- `msgPushUrl`：后端消息处理接口（该参数如果无后端无需配置）

	- **config-chatgpt.js**：
		- `CHATGPT_URL`：ChatGPT请求地址，参照官方，一般无需变动
		- `CHATGPT_API_KEY`：基于ChatGPT API进行调用，需要使用api_key才能调用。（新账号有5$3个月的额度，也可付费购买【现在ChatGPT账号含5美元也不贵】）
		-  `CHATGPT_MODEL`：使用的对话模型，如果开通了ChatGPT4，可以修改为对应的模型。默认gpt-3.5-turbo-16k
	- **config-proxy.js**:
		- `PROXY_HOST`：代理HOST，国内环境无代理无法访问
		- `PROXY_PROTOCOL`：代理HOST对应的协议
		- `PROXY_PORT`：代理HOST的端口
- 测试网络：`npm run test`：结果如下
  
<img width="50%" alt="测试网络结果" src="https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/fail.jpeg"/>

	>如果出现异常，检查代理是否正常，无法解决可留言

- 启动项目：
	- `npm run dev`:扫码即可启动专属微信机器人啦
  
<img width="50%" alt="扫码启动专属微信机器人" src="https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/success.jpeg"/>

> 有相关问题欢迎留言


------

**<center>三、目前缺陷</center>**

 1. wechaty获取的微信备注可能不准确
 2. 当前测试响应时间基本在5秒内，对于大请求可能会较慢
 3. 网络或是微信官方问题，存在掉线问题
 4. 目前NodeJS版本前端还没接入多轮对话，仅在自己的后端实现了多轮对话

------

**<center>四、未来功能</center>**

 1. 考虑使用场景，引入其他AI模型，如Claude等，目前在研究中
 2. 实现多轮对话

-----

> 获取自建免费ChatGPT链接地址：公众号关注【迷茫的21世纪的新青年】回复 新地址
> 
> 搭配获取Token：公众号关注【迷茫的21世纪的新青年】回复 token