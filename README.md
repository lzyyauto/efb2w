# efb2w
对于不愿意被微信app所统治,telegram重度使用者等理由  
ehForwarderBot是个很好的选择.可以帮你做信息聚合  
网络教程都是1.X,并且没有直接可用的Docker镜像(可能也是我没找到)  
于是自己就打包了一个,主要是针对微信  
如果有需求扩展.可以自行动手捣鼓  

有两个相关配置文件config.yaml
镜像里
- /root/.ehforwarderbot/profiles/default/
    ehforwarderbot的配置.镜像中只有简单的telegram,wechat组件

- /root/.ehforwarderbot/profiles/default/blueset.telegram/
    telegram组件配置.需要手动处理

# Getting Started

申请bot,这块我就不重复写了.引用自[葉子](https://niconiconi.fun/2018/03/17/install-efb-v2/)

>首先申请 bot api
以下这段信息引用自 efb 作者博客:[1a23](https://blog.1a23.com/2017/01/09/EFB-How-to-Send-and-Receive-Messages-from-WeChat-on-Telegram-zh-CN/)

>Telegram Bot 是 EFB（Telegram 主端）的出口，也是呈献给用户的渠道。我们在这里使用了 Telegram 官方的 Bot API，
以最大化利用 Telegram Bot 所提供的各种便利功能。

>要创建一个新的 Bot，要先向 @BotFather 发起会话。发送指令 /newbot 以启动向导。期间，你需要指定这个 Bot 的名称与用户名（用户名必须以 bot 结尾）。完毕之后 @BotFather会提供给你一个密钥（Token），妥善保存这个密钥。请注意，为保护您的隐私及信息安全， 请不要向任何人提供你的 Bot 用户名及密钥，这可能导致聊天信息泄露等各种风险。

>接下来还要对刚刚启用的 Bot 进行进一步的配置：允许 Bot 读取非指令信息、允许将 Bot 添加进群组、以及提供指令列表。

>发送 /setprivacy 到 @BotFather，选择刚刚创建好的 Bot 用户名，然后选择 “Disable”.

>发送 /setjoingroups 到 @BotFather，选择刚刚创建好的 Bot 用户名，然后选择 “Enable”.

>发送 /setcommands 到 @BotFather，选择刚刚创建好的 Bot 用户名，然后发送如下内容：

>link - 将会话绑定到
chat - 生成会话头
recog - 回复语音消息以进行识别
extra - 获取更多功能

>bot申请好后，请记住你的 Token ，然后到 @iloli_bot 处获取你的 ID 。 发送 /myid 给 @iloli_bot ，他会返回一串数字 ，那就是你的 ID
把你申请到的 Token 和你的 ID 保存好 接下来会用到

-------------------分割线-----------------------

`docker pull lzyyauto/efb2w`

配置文件
```
token: "12345678:1a2b3c4d5e6g7h8i9j"
#内替换为你在 @BotFather 处获得的 token
admins:
- 102938475
#后面的数字替换为你在 @iloli_bot 处获得的 id
```
保存为~/efb2w/blueset.telegram/config.yaml

`docker run --name=efb2w -v ~/efb2w/blueset.telegram/:/root/.ehforwarderbot/profiles/default/blueset.telegram/ lzyyauto/efb2w`

扫描登录即可.enjoy

PS:众所周知的原因.国内主机 or 自己的服务器还差一步连通telegram.自行解决

参考资料 [blueset/ehForwarderBot](https://github.com/blueset/ehForwarderBot) 
