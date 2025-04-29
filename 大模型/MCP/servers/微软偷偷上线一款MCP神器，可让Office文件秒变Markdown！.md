---
标题: "微软偷偷上线一款MCP神器，可让Office文件秒变Markdown！"
链接: "https://mp.weixin.qq.com/s/JB1GzR-7dKSGdTxSjfaFwA"
作者: "[[JJJohn]]"
创建时间: "2025-04-29T15:49:57+08:00"
摘要:
tags:
  - "clippings"
  - "mcp"
  - "office"
  - "markdown"
字数: "272"
状态: "未开始"
---
# [[学习方法/预读法介绍]]
### 预读问题  
**基于你的目标**：
- Q1: 
- Q2: 
- Q3:   

### 关键图表/代码  
![[提取的图表或代码片段]]
### 初步关联  
- 已知：[[已掌握的相关知识]]  
- 未知：`#待探索`  

### 输出目标
- [ ] 

### 总结
- 是什么
- 为什么
- 怎么用

# 内容
#flashcards

原创 JJJohn

2025-04-20 00:20:18

精确发文时间由壹伴提供

手机阅读

刚刚，微软悄咪咪上线了一个MCP服务器

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/M3PrhSUICnFGXrPf0slztsaHscYAAKly78lmRkTbIKb3dUN7JGdI6lQP9wXGlbQYvdiaicDc7gh5cO2KxUVfUKzw/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

这玩意专门用来把Office文件（PPT、Word、Excel）

**一键转成Markdown格式** ！

这对AI 工具链来说简直不要太香！

你可能要问，

这个叫 **markitdown-mcp** 的工具

到底是个啥？

有啥用？

值得这么激动？

先看看官方README

你别说，这玩意是挺有点儿意思！

基本上就是个 **轻量级STDIO和SSE的MCP服务器**

只暴露了一个工具： `convert_to_markdown(uri)`

这个uri可以是任意 `http:`、 `https:`、

`file:`或者 `data:`开头的URI

**使用起来巨简单** ：

```
pip install markitdown-mcp
```

一行命令就把它装上了

然后直接敲：

```
markitdown-mcp
```

就能启动MCP服务器（默认用STDIO模式）

如果想用SSE模式启动，也行：

```
markitdown-mcp --sse --host 127.0.0.1 --port 3001
```

@AndrewV 在评论区表示：

「现在Adobe需要悄悄推出一个PDF的MCP」

（确实，PDF向来是AI处理的老大难）

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/M3PrhSUICnFGXrPf0slztsaHscYAAKlytJAOf6cXHL9iciaxm8Yk35jjc5rD7ZOe0HCdzFt4kzA8hiavZrjB6Vnag/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

@bruno激动到直接狂发"wow wow wow wow"

（这么开心，看来之前是被文件处理折磨惨了）

还有老哥@Jiemji好奇地问：

「那从markdown转回office格式呢？」

（这个问题好，不过……兄弟你可能想多了）

而为什么这工具会这么受欢迎？

关键在于它和 **Claude Desktop** 的完美配合

根据文档，只要简单设置一下

Claude就能直接调用这个工具

处理各种文件格式！

你只要按照https://modelcontextprotocol.io/quickstart/user#for-claude-desktop-users 里的指引

去找到 `claude_desktop_config.json` 文件

往里面加这么一段：

```
{
  "mcpServers": {
    "markitdown": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "markitdown-mcp:latest"
      ]
    }
  }
}
```

搞定！

从此Claude就能直接读懂你的文件了

想挂载本地目录给它读？

也不难：

```
{
  "mcpServers": {
    "markitdown": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "-v",
        "/home/user/data:/workdir",
        "markitdown-mcp:latest"
      ]
    }
  }
}
```

这下好了， `/home/user/data` 目录下的所有文件

都能被Docker容器里的工具访问到了

而评论区老哥@corytomlinson直接开杠：

「 **这明明就是个Python库，为啥要加抽象层？**

**MCP就是代理领域的LangChain** 」

@Fer立马反驳：「 **你没懂重点，人类会读文档用工具，**

**但AI代理需要自己发现工具并理解用法，**

**所以协议是必需的** 」

楼主matt palmer也下场解释：

「 **每个MCP服务器都是库的抽象。**

**与其写"if x then do y"这样的代码，**

**不如直接告诉GPT"请总结这个PDF"，**

**它就能做到，因为它有了工具** 」

（这才是重点啊！ **用工具才是正道** ）

@Asher Cohen 也提出了一个大家都关心的关键问题：

「 **这些工具总说能提取文本，**

**但从来不说图片怎么处理。**

**图片也很重要啊！** 」

（确实是个问题，不过看README，

这个工具处理的是文件URI，

图片模态的识别自然是没有的）

对了，官方还提供了Docker支持

可以用这个命令构建镜像：

```
docker build -t markitdown-mcp:latest .
```

然后这样运行：

```
docker run -it --rm markitdown-mcp:latest
```

这样远程URI就能处理了

要想访问本地文件？

挂载一下目录就行：

```
docker run -it --rm -v /home/user/data:/workdir markitdown-mcp:latest
```

而如果想调试这个MCP服务器？

还有专门的 `mcpinspector` 工具：

```
npx @modelcontextprotocol/inspector
```

然后通过指定的主机和端口连接

（比如 `http://localhost:5173/` ）

就能进行实时调试了

不得不说，是挺周到的

@NeuralCat在评论区问：这个工具真有这么重要？

Ask Perplexity解释道：

「 **MarkItDown-MCP让你能即时将Office文件转为Markdown，**

**方便整合到纯文本工作流、接入LLM，**

**或发布内容到网络上** 」

「 **对互操作性是个大进步——**

**因为Markdown轻量、广泛支持，**

**且大多数AI模型原生理解，**

**这个工具搭起了专有格式和开放、**

**对AI友好的文本之间的桥梁** 」

（说白了就是 **让AI更好地理解文件内容** ）

我来总结下这工具的最大亮点：

一是 **开箱即用** ：pip安装一下就能跑

二是 **支持多种URI** ：本地文件、网络文档都行

三是 **无缝集成Claude Desktop** ：配置简单明了

四是 **容器化部署** ：Docker一键启动

用AI工具赋能知识工作者，且能大规模应用！

这波操作 **降低了技术门槛**

这就是 **数据与AI的粘合剂** 啊！

之前喂文件给AI，那叫一个费劲

要么复制粘贴，格式全乱

要么自己写解析代码，累死人

现在？

让AI自己调用工具去读就完事儿了！

**对AI开发者来说，这简直是重大福利啊**

别的不说，这波微软操作真实在

出品方是AutoGen团队，就是那个

专注于开发Agent框架的微软团队

难怪能把工具做得这么实用

最后说一句：

**这玩意有安全隐患吗？**

README里提醒说：

「 **服务器不支持身份验证，**

**且以运行它的用户权限运行。**

**因此，在SSE模式下，**

**建议将服务器绑定到localhost（默认）** 」

要想试试的一话

官方地址在此：https://github.com/microsoft/markitdown

PyPI包名在此：markitdown-mcp

快装一个试试吧

你的AI工作流

从此就能少掉一堆痛苦了！

👇

👇

👇

另外，我还用AI 进行了全网的AI 资讯采集，并用AI 进行挑选、审核、翻译、总结后发布到《AGI Hunt》的知识星球中。

这是个只有信息、没有感情的 AI 资讯信息流（不是推荐流、不卖课、不讲道理、不教你做人、只提供信息）

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/M3PrhSUICnHPqujshkiaWeLN2xqWy9RWexNwDrIT9ictY61Q8LOJLVfhkhZIT1Yt4dP0cN3yxAe1NbbCszvZKIicA/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

![图片](https://mmbiz.qpic.cn/sz_mmbiz_jpg/M3PrhSUICnFGXrPf0slztsaHscYAAKlygaOk1ZAdTicicoHApAnr6vqeG3GHPTDdzb8EarXxz7gXWIickMEKEMDeQ/640?wx_fmt=jpeg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1)

  

  

[阅读原文](https://mp.weixin.qq.com/s/)

继续滑动看下一个

AGI Hunt

向上滑动看下一个

![](https://mp.weixin.qq.com/s/assets/imgs/data-enhance/isok.svg) 订阅成功