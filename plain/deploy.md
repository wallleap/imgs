# 部署

- 由于使用的 Vue-Router 的 WebHistory 模式，因此需要设置重定向，否则直接刷新会 404
- 直接在线部署则需要添加环境变量

## Nginx 重定向

可以直接将打包结果上传到 Nginx 服务器，之后修改一下当前网站的 Nginx 配置

添加重定向代码

```nginx
location / {
  try_files $uri $uri/ /index.html;
}
```

## Vercel 重定向

直接从 GitHub 导入 plain 仓库，需要在根目录添加 `vercel.json` 文件，可以通过自定义打包命令实现，例如把 build 命令改成

```sh
pnpm run build && echo '{
  "rewrites": [{ "source": "/:path*", "destination": "/index.html" }]
}' > vercel.json
```

## Netlify 重定向

直接从 GitHub 导入 plain 仓库，需要在打包结果里添加 `_redirects`，可以通过自定义打包命令实现，例如把 build 命令改成

```sh
pnpm run build && cd dist && echo '/*   /index.html   200' > _redirects
```

## Vercel 和 Netlify 环境变量

找到 Environment variables 选择导入 `.env` 文件或直接粘贴到文本框中，复制下面的内容进行修改粘贴，然后直接提交

```
# [必须配置] TOKEN，不配置获取不到文章，创建链接 <https://github.com/settings/personal-access-tokens>
V_GITHUB_TOKEN=""       # GitHub Token 中间任意地方逗号空格断开，否则直接上传到 GitHub 会失效，例如 V_GITHUB_TOKEN="github_pat_11AKLZALQ0ZMxAPQczeVsa_fsrO5ic22IhiUiE, l1F9VheIQQAT3eIJV91frYyTgCnWJNJEJ6A6nkvdKraQ"
# [必须配置] GitHub Issues 用于展示文章
V_USERNAME=""           # GitHub 用户名，例如 wallleap
V_REPOSITORY=""         # Issues 所在仓库名，例如 myblogs
# [可选] 友链仓库，如果是在博客仓库里设置的评论，这里就不用管
# V_FRIENDS_REPO="friends"

# [必须配置] 博客信息
V_TITLE=""              # 博客标题，例如 V_TITLE="wallleap"
V_DESCRIPTION=""        # 博客描述，例如 V_DESCRIPTION="主要分享前端知识"
V_KEYWORDS=""           # 博客关键词，例如 V_KEYWORDS="前端, web, 博客"
V_LOGO="./logo.svg"     # 博客 Logo，直接替换 public 中 logo.svg 文件即可

# [可选配置] LeanCloud 用于文章阅读量统计，链接 <https://console.leancloud.app/> 创建应用并把自己的域名添加到 安全中心-Web 安全域名
V_LEANCLOUD_ID=""       # APP_ID，例如 V_LEANCLOUD_ID="p5t88r7y7SNhoIW7Y0tnXOI9-MdYXbMMI"
V_LEANCLOUD_KEY=""      # APP_KEY，例如 V_LEANCLOUD_KEY="i65OGuk90hCZ2GK8BCtJsKMf"
V_LEANCLOUD_SERVER=""   # REST API 服务器地址，需要绑定自己的域名，例如 V_LEANCLOUD_SERVER="https://leancloud.uicop.com"

# [可选配置] 建站时间
V_CREATED_TIME=""       # 格式 YYYY-MM-DD，例如 2024-12-31

# [可选] 您的信息 在底部显示
V_AUTHOR=""   # 你的名字，例如 V_AUTHOR="luwang"
V_EMAIL=""    # 你的邮箱，例如 V_EMAIL="luwang@oicode.cn"
V_LINK=""     # 你的个人网站，例如 V_LINK="//luwang.info"
V_GITHUB=""   # 你的 GitHub 链接，例如 V_GITHUB="//github.com/wallleap"

# [必须] 友链信息 友链页展示
V_NAME=""     # 你的博客名字，例如 V_NAME="wallleap"
V_URL=""      # 你的博客地址，例如 V_URL="//myblog.wallleap.cn"
V_AVATAR=""   # 你的头像，例如 V_AVATAR="//cdn.wallleap.cn/img/avatar.jpg"
V_DESC=""     # 你的博客描述，例如 V_DESC="Luwang's Blog"

# [可选] 评论配置 Utterances 代码，前往 https://utteranc.es/ 获取代码
V_UTTERANCES_CODE=``  # 例如 V_UTTERANCES_CODE=`<script src="https://utteranc.es/client.js" repo="你的用户名/comments" issue-term="title" label="Comment" theme="github-light" crossorigin="anonymous" async></script>`

# [可选] 一页显示的博客数量，尽量填大一点，避免博客文章显示不全
V_BLOG_COUNT="80"
# [可选] 一页显示的友链数量，尽量填大一点
V_FRIEND_COUNT="50"

# [可选] ICP 备案
V_ICP=""
V_ICP_LINK=""
# [可选] 公安备案
V_BEI=""
V_BEI_LINK=""
```

Vercel 的粘贴到这

![](https://private-user-images.githubusercontent.com/43487278/400295388-f244ef9d-8db5-4b67-9267-6601ec2677d6.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Mzk4NjUxOTcsIm5iZiI6MTczOTg2NDg5NywicGF0aCI6Ii80MzQ4NzI3OC80MDAyOTUzODgtZjI0NGVmOWQtOGRiNS00YjY3LTkyNjctNjYwMWVjMjY3N2Q2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTAyMTglMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwMjE4VDA3NDgxN1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTQ3NDYyOWYxOWZkYmVjNjYyN2JlYmZlOGFhNjBkZTk1ZDJjMjg2YWNhZmYzZjgxNzBjOWRhZDBkZDhiZjEzZTMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.XaTDHtdjl0GpYK6Ja_ZgukEtDXoObJ0--VjnvVlmzUE)

Netlify 的

![](https://private-user-images.githubusercontent.com/43487278/413744157-e75a0f7d-622d-477c-b74e-5af9ecd3931d.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Mzk4NjQ5OTEsIm5iZiI6MTczOTg2NDY5MSwicGF0aCI6Ii80MzQ4NzI3OC80MTM3NDQxNTctZTc1YTBmN2QtNjIyZC00NzdjLWI3NGUtNWFmOWVjZDM5MzFkLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTAyMTglMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwMjE4VDA3NDQ1MVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWRmZTVjMjRmNmY2N2NkZDU2ZDNjZDE2NGQ1NjBmZjE3NmFmN2IxZmYzZjFiMjg3OGUxMjU5YzA1MWFiOTIwMTgmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.eW_VtmspZ7mNHHIRIMBhNCzdNHCp97HS692F35d8-_Q)
