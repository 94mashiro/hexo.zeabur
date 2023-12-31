---
title: 周刊 01 期
---
一个成功的 Blog，到底要经历多少次 Hello World 才是一个头。

## 1. Zeabur

Serverless 是一个很火的概念，他允许开发者即使没有自己的服务器也能部署应用。Heroku、Netlify、Vercel 都是目前很火的 Serverless 部署平台。

![Serverless](https://img.alicdn.com/tfs/TB1dQzBOwHqK1RjSZFkXXX.WFXa-2152-1557.png_.webp)
但这些平台通常都是比较偏向前端应用，他给了前端开发者极简的部署体验，只要关联 Git 仓库，平台就能通过仓库中的某些信息知道对应的框架类型，直接进行对应的部署操作。但是这种纯粹的极简也给了平台比较大的局限性，以至于很难进行其他类型应用的部署。

本文提到的 Zeabur 是一种以 Docker 为基础的部署平台，类似的平台还有 Railway。但是 Zeabur 应该是国人团队开发，所以对亚洲开发者这边的支持会好一点。目前 Zeabur 支持三个地区的部署（美国、香港地区、台湾地区），本站也是部署在了 Zearbur 的香港地区（底层是用了 AWS）。

Zeabur 应用的部署非常简单，只需要提供一个 dockerfile，应用就能跑起来。正好 Typecho 也有对应的 Docker 镜像，那就照葫芦画瓢写一份极简的 dockerfile 吧，如下：

```dockerfile
FROM joyqi/typecho:nightly-php7.4-apache
COPY ./usr /usr/src/typecho/usr/
EXPOSE 80
```

提交到 Git 仓库后，就可以在 Zeabur 中以 Git 的方式创建一个服务了。

![创建服务](https://cdn.te.sb/202310161858586.png)

这时候服务会启动，然后根据 Dockerfile 里的内容，进行镜像的拉取和执行。不用管它，因为现在还需要去新建一个数据库。
Zeabur 也提供了一些预设的服务，当然包括数据库，我们选择 Prebuild 类型，就能搜索到 PostgreSQL（当然你也可以用 MySQL）。

![创建 PostgreSQL 服务](https://cdn.te.sb/202310161902065.png)

得益于 Docker 的能力，创建数据库服务很快，通常几秒就能搞定。
然后我们就需要将数据库配置通过环境变量的方式配置给 Typecho 服务，配置完成后，我们只需要给服务配一个域名就可以了。

![配置环境变量](https://cdn.te.sb/202310161904293.png)

这样，一个不需要购买服务器就能在互联网上运行的 Typecho 应用就成功部署了，是不是很方便？
如果你也希望使用这种方式部署你的 Docker 应用，可以使用我的 [AFF](https://zeabur.com?referralCode=MashiroWang) 进行注册，这是对我的支持，谢谢。

## 2. 更新桌搭 1.0

![桌搭1.0](https://cdn.te.sb/202310182310358.jpeg)

首先解释一下 1.0 的原因，其实在两年前就有了升降桌和双屏，但那时候的桌面就非常乱，看起来就像是另一个工位一样。因为没有动力，所以乱糟糟的状态持续了好久，也就配不上一个正式的版本号了。

这个桌面主要承担了 PC 主机的娱乐需求，和 MacBook 的办公需求。
对于 PC 的显示信号，主要是由 DP 线来承担，而 MacBook 的显示信号，则由 Type-C 进行传输。我也为 MacBook 配了一个 CalDigit DS4，通过一根雷电 4 线来承担充电、视频信号和数据信号的传输。

最近入手了一台 HIFIMAN 的小夜曲，是一个解码耳放，说实话非常占地方，这么多设备对于一个 1.5 M 宽的桌面已经有些拥挤了。所以借此契机，有了一个整理桌搭的想法了。

其实我觉得桌搭很简单，将一些东西归归类放放好，主打一个各就各位，空间利用，这样一个令人满意的桌搭就实现了。

我这边的想法也比较简单，就是尽可能利用一下主显示器下面的空间，由于这个显示器的支架底座面积非常大，导致本身显示器下方放不下很多东西。解决这个问题也比较简单，要么是买一个显示器摇臂，要么就买一个显示器增高架。

由于我的主显示器是 32 寸的，本身就非常重，超过了一般摇臂的可承受重量范围，能用的艾格升的价格又非常美丽，所以主显示器我一直没有使用摇臂。于是这次我也选择了比较廉价的方案，在淘宝买了一个实木的增高架，选的胡桃木，收到之后看到实物质感也非常不错。用上了增高架之后，增高架下方的空间就顺理成章的可以放入我的 DS4 以及小夜曲了。

这样桌面上的大多数物件都占据了桌面中间的 30% 的区域，而左侧和右侧的区域被我放置了 MacBook 以及耳机。

这样，一个干净且适合我的桌面就布置完毕了，由于我也不是一个爱折腾桌面的人。所以如果不是因为什么原因一定要改变桌面布局的话，这个桌搭可能就会一直延续下去了，哈哈，适合自己的就是最好的。
