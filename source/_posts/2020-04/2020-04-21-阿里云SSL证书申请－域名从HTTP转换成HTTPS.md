---
title: 阿里云SSL证书申请－域名从HTTP转换成HTTPS
date: 2020-04-21 09:49:06
categories:
  - [博客, 环境安装]
tags:
---

阿里云SSL证书申请－域名从HTTP转换成HTTPS
### 背景
1. 购买域名shendawei.cn搭建部署博客后，一直用http协议，网站安全性很低
2. 想认真学习网站协议的知识概念及应用场景使用
3. 一直想找个合适的契机，把自己的域名http转换为https
4. 近两天，对博客配置了hexo-blog-encrypt插件，加密文章部署到服务器域名后，输入密码无反应，阻塞加密文章阅读，严重影响博客使用
故今天下定决心，系统学习下阿里云SSL证书文档手册。
<!--more-->

### 阿里链接
[阿里云SSL证书文档手册](https://help.aliyun.com/product/28533.html?spm=a2c4g.11186623.6.540.26b05927ZyyVB3)
### 基本概念记录
SSL证书
> 阿里云SSL证书服务（Alibaba Cloud Certificates Service）是阿里云联合若干国内外知名CA证书厂商，在阿里云平台上直接提供服务器数字证书，阿里云用户可以在云平台上直接购买甚至免费获取所需类型的数字证书，一键部署在阿里云产品中，最小成本的将所持服务从HTTP转换成HTTPS。

[HTTPS与HTTP有什么不同？](https://help.aliyun.com/document_detail/42229.html?spm=a2c4g.11186623.2.25.313b5fb77kOXWp#concept-mpn-q4p-ydb)
[哪些网站必须启用HTTPS加密？](https://help.aliyun.com/document_detail/42220.html?spm=a2c4g.11186623.2.27.313b5fb77kOXWp#concept-sx4-pdv-ydb)
* 电商平台及其相关支付系统网站
* 银行系统、金融机构等高私密性网站
* 政府、高校、科研机构及其相关网站
* 以搜索引擎为主要流量来源的网站
* 以邮箱为主的企业交流平台
* 包含个人重要信息的博客等个人网站

[各类SSL证书的区别和网页展示效果](https://help.aliyun.com/document_detail/44788.html?spm=a2c4g.11186623.2.43.313b5fb77kOXWp#concept-bkt-v4p-ydb)
无证书网页展示效果(http协议)
{% qnimg /2020-04-21-阿里云SSL证书申请－域名从HTTP转换成HTTPS/20200421100905355.png %}
[如何选择：证书类型-证书品牌-保护域名数量？](https://help.aliyun.com/knowledge_detail/48020.html?spm=a2c4g.11186623.4.2.1d3d2d23CKZCd2)
[阿里云证书品牌](https://help.aliyun.com/document_detail/28542.html?spm=a2c4g.11186623.2.13.2e1c6872JKJFMi#title-esd-zc5-4e5)
[主流数字证书都有哪些格式？](https://help.aliyun.com/knowledge_detail/42214.html#concept-a4g-mbv-ydb)
[SSL证书安装指南](https://help.aliyun.com/knowledge_detail/95505.html?spm=a2c4g.11186623.4.4.1d3d2d23CKZCd2)
> 说明 如果证书是在阿里云的产品上使用，建议下载Nginx服务器版本的证书。

[申请免费证书](https://help.aliyun.com/document_detail/148895.html?spm=a2c4g.11186623.6.631.313b5fb7TsZeAI)
[在Nginx/Tengine服务器上安装证书](https://help.aliyun.com/document_detail/98728.html?spm=a2c4g.11186623.2.12.2861625aSYtNdT#concept-n45-21x-yfb)

### 实际安装免费SSL证书
* 购买证书
登录控制台－产品服务点SSL证书，进入SSL证书控制台－购买证书－进入云盾证书服务，选择免费版（个人）DV类型，证书品牌：赛门铁克（Symantec）－DV类型仅支持一个域名，购买数量自己可选，时长只能1年－确认订单－确认支付(0.00)－恭喜，支付成功 请登录控制台，申请证书，签发成功后，可安装到网站/APP/邮箱等使用。
* 申请证书
[证书申请和应用流程](https://help.aliyun.com/document_detail/143013.html?spm=a2c4g.11186623.6.572.1d7b6872kWr0XU)
    * 域名验证方式
    自动DNS验证
> 您当前账号下的域名与云解析都在阿里云可以使用自动验证
    * CSR生成方式
    系统生成
> CSR文件是您的公钥证书原始文件，包含了您的服务器信息和您的单位信息，需要提交给CA认证中心审核。建议您使用系统创建的CSR，避免因内容不正确而导致的审核失败。

* 验证证书
    * 添加域名DNS解析，系统自动添加以下记录类型
    记录类型 TXT
    主机记录 _dnsauth
    记录值 202004200000005xzq1s5qe8g4w42ahabhsk9t08h9jekjtdxk8yuqaibc76u5xn
    * 点击验证
       验证成功
    * 邮件查收，等待审核
* 等待签发证书
    约1小时
    短信通知签发成功
* 下载证书并安装至Web服务器
    nginx blog
> 您有一张证书从控制台下载，为确保您的安全性，请确认是否是您本人操作。
证书名称： cert-3594245
证书域名:    shendawei.cn, www.shendawei.cn
下载时间：2020-04-21 11:59:34