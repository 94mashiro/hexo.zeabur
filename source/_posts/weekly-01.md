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
