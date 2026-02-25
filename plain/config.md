# 配置中的一些值

## V_GITHUB_TOKEN

> 用于获取 issue，包括文章列表、文章详情、文章详情页评论展示、关于页、友链信息等

直接前往 <https://github.com/settings/personal-access-tokens> 生成一个新的 Token

- Repository access 选择 issue 所在仓库，例如 `myblogs`
- Permissions 添加 Issues 并且修改成 Read and write

将 Token 从中间用空格逗号分开，填写到后面

例如获取到的 Token 如下

```
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
```

随便从中间分开

```
V_GITHUB_TOKEN="github_pat_11AKLZALQ0THGC7QD3oXiK_1yC1MANz, FCMnRjvoM5x3gVG7525rqh3RAqlx1j4ZX1IZOMDVWUH5Xy8WW02"
```

## Utterance 评论

> 友链页的评论

在 GitHub 新建一个仓库，例如 `comments`，前往 <https://utteranc.es/>，在 Repo 处输入 `你的用户名/comments`，然后下划到下面，点击 Copy 复制代码

将回车删掉，换成空格，让代码在一行，之后粘贴到 V_UTTERANCES_CODE 配置项中

---

以下是一个最基础的 `.env.local` 配置

```
# [必须配置] TOKEN，不配置获取不到文章，创建链接 <https://github.com/settings/personal-access-tokens>
V_GITHUB_TOKEN="github_pat_11AKLZALQ0vHLl7wB22QgB_0LA0h, Wp0gbcUwbWa8DDa2bYPzoDV1svPifDL60LS9pL2O3Q2I7UqDXdx4RH"
# [必须配置] GitHub Issues 用于展示文章
V_USERNAME="wallleap"           # GitHub 用户名，例如 wallleap
V_REPOSITORY="blogtest"         # Issues 所在仓库名，例如 myblogs
# [可选] 友链仓库，如果是在博客仓库里设置的评论，这里就不用管
# V_FRIENDS_REPO="friends"

# [必须配置] 博客信息
V_TITLE=""              # 博客标题，例如 V_TITLE="wallleap"
V_DESCRIPTION=""        # 博客描述，例如 V_DESCRIPTION="主要分享前端知识"
V_KEYWORDS=""           # 博客关键词，例如 V_KEYWORDS="前端, web, 博客"
V_LOGO="./logo.svg"     # 博客 Logo，直接替换 public 中 logo.svg 文件即可

# [可选配置] 建站时间
V_CREATED_TIME=""       # 格式 YYYY-MM-DD，例如 2024-12-31

# [可选] 您的信息 在底部显示
V_AUTHOR=""   # 你的名字，例如 V_AUTHOR="luwang"
V_EMAIL=""    # 你的邮箱，例如 V_EMAIL="luwang@oicode.cn"
V_LINK=""     # 你的个人网站，例如 V_LINK="//luwang.info"
V_GITHUB=""   # 你的 GitHub 链接，例如 V_GITHUB="//github.com/wallleap"

# [必须] 友链信息 友链页展示
V_NAME="wallleap"     # 你的博客名字，例如 V_NAME="wallleap"
V_URL="//myblog.wallleap.cn"      # 你的博客地址，例如 V_URL="//myblog.wallleap.cn"
V_AVATAR="//cdn.wallleap.cn/img/avatar.jpg"   # 你的头像，例如 V_AVATAR="//cdn.wallleap.cn/img/avatar.jpg"
V_DESC="Luwang's Blog"     # 你的博客描述，例如 V_DESC="Luwang's Blog"

# [可选] 评论配置 Utterances 代码，前往 https://utteranc.es/ 获取代码
V_UTTERANCES_CODE=``  # 例如 V_UTTERANCES_CODE=`<script src="https://utteranc.es/client.js" repo="你的用户名/comments" issue-term="title" label="Comment" theme="github-light" crossorigin="anonymous" async></script>`

# [可选] 一页显示的博客数量，尽量填大一点，避免博客文章显示不全
V_BLOG_COUNT="120"
# [可选] 一页显示的友链数量，尽量填大一点
V_FRIEND_COUNT="80"

# [可选] ICP 备案
V_ICP=""
V_ICP_LINK=""
# [可选] 公安备案
V_BEI=""
V_BEI_LINK=""
```
