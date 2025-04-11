---
标题: "从RestAPI到MCP：Higress AI网关一键切换"
链接: "https://mp.weixin.qq.com/s/xfdXZ3-j-WYrxnxEvmQVMA"
作者: "[[阿畅]]"
创建时间: "2025-04-11T11:14:10+08:00"
摘要: "文章介绍了从RestAPI到MCP的Higress AI网关一键切换方法及其配置步骤。"
tags:
  - "clippings"
  - "AI"
  - "Higress"
  - "MCP"
  - "网关配置"
  - "编程"
字数: "21"
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
1、先来一个Higress AI网关在整体方案中的位置

![0](https://mmbiz.qpic.cn/mmbiz_png/M99nibPde1RtWL428QicUR5Is2KwToYOOficeAGqV8kicWqqM06sC1cHhTIdDyEGGHlE5WIic4aqmwcYT5vDHfswWqA/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

2、Higress MCP Server 快速开始

![0](https://mmbiz.qpic.cn/mmbiz_png/M99nibPde1RtWL428QicUR5Is2KwToYOOfXSf350h5Kmhvhib2GibJAGoDIBw8eiaOkmdJXsCBr9G7htb6vM6uEVV7Q/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

3、启动MCP插件及对应接口配置

![0](https://mmbiz.qpic.cn/mmbiz_png/M99nibPde1RtWL428QicUR5Is2KwToYOOfQbyDcUTPv0rnTIfhLiaxZTQtl99WUnhEnbUdibhme4aShAn91sHNFCLQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

4、MCP服务转换的模版文件

![0](https://mmbiz.qpic.cn/mmbiz_png/M99nibPde1RtWL428QicUR5Is2KwToYOOfYZgpoLT89tZoHG3CNOYq81PwyMuZz9ohnibibNAS9Alv7f2xm4R2gwhQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

5、有一个前提条件和注意点，需要配置全局参数配置 （像ChatWise 支持 MCP streamable HTTP 协议就不需要配置全局 ConfigMap 配置）

![0](https://mmbiz.qpic.cn/mmbiz_png/M99nibPde1RtWL428QicUR5Is2KwToYOOfzKq2ic7pVK0iaMN4eYfvKPHlibicSVicHsa2VQmtdypBnUh1jMviaOQPicicmw/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

PS:写在最后，回复“Higress”，查看REST API 转换MCP 服务详细配置说明，欢迎喜欢AI的朋友，加微信多多交流。