---
title: 使用hexo建立博客
date: 2019-06-14 16:29:34
comments: true
tags:
---

大概每个cs engineer都有一个blog情怀，要做一个自己的站点。在查找资料的过程中，近期总是有意无意的注意到。
{% asset_img powered-by-hexo.png hexo %}

## hexo是什么？它能做什么？它有什么特点？
快速、简洁且高效的博客框架
- 超快速度
- 支持Markdown
- 一键部署
- 丰富的插件

## 用hexo建设blog站点流程
万事开头难，把hexo部署到github pages上面对于熟悉github的同学并不难。但是对于第一次接触pages，或非cs行业的同学还稍有难度。
### hexo在本地建立站点

### hexo将站点推送github
### hexo绑定自己的域名
1. 注册自己的域名
注册域名需要像域名商的网站商发起购买。在它的网站上筛选到喜欢的域名如果尚未出售就可以直接购买。如果已经售出那么除非你真的志在必得，否则还是推荐换一个。那么我们要在哪个域名商店铺里进行购买呢？类比于网购我们可以去淘宝、京东、拼多多，域名商店也有很多。hanadumal.com我是在namesilo上购买的。我使用过的域名购买有阿里云、godaddy、namesilo。国内的暂且不表了。godaddy这家伙是在是坑，虽然是我买过最多的一家，但是现在已经完全不会考虑从godaddy再买了。首先价格很高，第一年通常会有优惠，但是如果你一次购买大于一年，后面的年费比其他家高很多。举例来说，hanadumal.com我在godaddy上查询，发现购买价格是470+。续费价格更贵，在godaddy一上车购买一年试试水，你会发现第二年快到期续费的时候居然比一开始买两年的第二年价格高很多。隐私保护还要额外收费60元/年。namesilo上我买的第一年6.99到，续费8.99刀/年。即使按照人民币汇率7来简单估算，5年都按照8.99刀，折合人民币也只要315元不到。另外namecheap也可以，价格比namesilo稍微贵一点，但是比godaddy良心的多。namecheap和namesilo都提供免费的隐私保护（永久)。我这里打开namecheap其实比namesilo快很多，感觉商店UI也更亲人。如果不在乎稍微多花钱namecheap也是不错的选择，如果第一关心的要点是性价比，那直接namesilo就对了。
` namesilo支持支付宝付款 `

> https://www.namesilo.com/index.php
> https://zhuanlan.zhihu.com/p/33921436

2. 修改域名的DNS解析
参照DNS提供商来进行域名的A记录操作。以namesilo为例。
a) 创建A记录，来把你的域名指向到以下几个IP
- 185.199.108.153
- 185.199.109.153
- 185.199.110.153
- 185.199.111.153

在namesilo上的操作为：

b) 等一段时间，我大概等了两个小时才生效。用dig命令来验证你的domain解析。


3. 设置github仓库的custom domain
> https://help.github.com/en/articles/quick-start-setting-up-a-custom-domain
> https://help.github.com/en/articles/adding-or-removing-a-custom-domain-for-your-github-pages-site
> https://help.github.com/en/articles/about-supported-custom-domains
> https://help.github.com/en/articles/setting-up-an-apex-domain
> https://help.github.com/en/articles/setting-up-an-apex-domain-and-www-subdomain
> https://help.github.com/en/articles/custom-domain-redirects-for-github-pages-sites
{% asset_img 404.png Github Pages 404 Error. %}

## 配置next主题
> https://theme-next.iissnan.com/getting-started.html

## 参考
> https://www.jianshu.com/p/35e197cb1273


## FAQ
1. hexo server -p 8080 后访问http://localhost:8080不到页面?

2. scaffolds有什么用?
   scaffolds是脚手架，或者说是创建posts时使用的模版。当执行了hexo new photo 'My Gallery'以后，会在scaffolds目录下寻找
   photo.md作为创建source/_posts/My-Gallery.md的模版。
   
3. deploy到github以后，通过<xxxx>.github.io访问点击进入文章详情，提示404。
   我遇到过的情况是，浏览器本地缓存导致的，清空缓存或者换个浏览器可以正常访问。部署到github以后，用<xxxx>.github.io来访问一般不会出现问题。
   
4. 绑定域名DNS解析A记录、CNAME以后，通过新绑定的域名访问，提示404。
   一个有可能的原因是，project的_config.yml修改了url配置, 修改后重新发布，访问正常。
   ```yaml
   url: http://hanadumal.com
   ```
   
5. 如何在hexo的markdown写作中插入图片?
   a) 如果图片少可以在
   b) 如果图片多，或者想比较系统的组织图片，你可以开启hexo项目的post_asset_fold配置。这也是我比较推荐的操作方式，只要一直按照设定的规则来操作，未来图片数量增长起来才不会难以维护。
   ```yaml
    post_asset_folder: true 
   ```
   > https://hexo.io/zh-cn/docs/asset-folders.html
   
6. 在draft中写作的过程中，如何能够在localhost进行查看?
   


