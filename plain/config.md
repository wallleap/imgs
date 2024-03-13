# 配置中的一些值

## V_GITHUB_TOKEN

直接前往 <https://github.com/settings/tokens> 生成一个新的 Token

将 Token 从中间用空格逗号分开，填写到后面

例如获取到的 Token 如下

```
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
```

随便从中间分开

```
V_GITHUB_TOKEN="github_pat_11AKLZALQ0THGC7QD3oXiK_1yC1MANz, FCMnRjvoM5x3gVG7525rqh3RAqlx1j4ZX1IZOMDVWUH5Xy8WW02"
```

## LeanCloud 相关

前往 <https://console.leancloud.app/> 注册国际版帐号，新建一个应用

点击设置-应用凭证，将 AppID、AppKey 的值复制后分别填入 V_LEANCLOUD_ID、V_LEANCLOUD_KEY

点击设置-域名绑定，绑定自己的域名，并配置好 CNAME 域名解析，部署证书（时间略久），之后将你的 API 访问域名填入 V_LEANCLOUD_SERVER，例如 `https://api.leancloud.wallleap.cn`

接下来点击设置-安全中心，把你博客的网址填写到 Web 安全域名中，注意需要加上 https 或 http

点击数据存储-结构化数据，点击创建 Class，新建两个 Class，名称分别为 `Counter` 和 `Visitor`，选择无限制，点击创建

## Utterance 评论

在 GitHub 新建一个仓库，例如 `comments`，前往 <https://utteranc.es/>，在 Repo 处输入 `你的用户名/comments`，然后下划到下面，点击 Copy 复制代码

将回车删掉，换成空格，让代码在一行，之后粘贴到 V_UTTERANCES_CODE 配置项中
