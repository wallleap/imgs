# 新建需要的 issues

<https://github.com/wallleap/plain>

## 友链页面

新建一个 issue，如图，点击 `Issues`，之后点击 `New issue`

![new issue](https://raw.githubusercontent.com/wallleap/imgs/main/plain/new-issue.png)

按图随便输入标题内容，创建 Label 名字为 `Friend`（这个必须一致），颜色随便，之后提交

![friend issue](https://raw.githubusercontent.com/wallleap/imgs/main/plain/friend-issue.png)

点击 `close issue`，将 issue 设置为关闭状态

![close issue](https://raw.githubusercontent.com/wallleap/imgs/main/plain/close-issue.png)

### 新建友链

之后在这个 issue 下新建的每条 Comment 都是友链，格式如下：

```json
{
  "name": "博客名",
  "url": "博客链接",
  "avatar": "头像链接",
  "desc": "博客描述",
  "tag": {
    "name": "标签名",
    "color": "标签颜色",
    "bg": "标签背景色"
  }
}
```

可以参考我的：<https://github.com/wallleap/myblogs/issues/1>

## 关于页面

接着新建一个 issue，点击右上角 `New issue`

- 标题随意
- 内容按照 markdown 语法写就行
- Label 必须设置为 `About`

## 博客文章

后面新建的所有的 issue 只要保持 `open` 状态，就都是博客文章

- 标题会默认设置为博客标题（没设置 front-matter 的情况）
- 设置除了 `About`、`Friend` 的 Label 将作为文章标签显示
- 设置的 Milestone 将作为文章的分类，如果不需要可以不设置
- 内容将作为博客文章的内容，请使用 markdown 语法编写

带 front-matter 的示例：

```md
---
title: 写主题会上瘾，一个简约主题 plain
date: 2024-03-10 10:07
updated: 2024-03-10 19:18
---

这里是博客文章内容，第一段将作为摘要显示。

## 标题1

段落

## 标题2

段落
```

如果在 front-matter 中设置了 `title`，那么将替换之前的标题；`date` 和 `updated` 分别作为文章的创建时间和更新时间
