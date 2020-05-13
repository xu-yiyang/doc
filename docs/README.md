# 怎么部署git项目
  1.登录 github  
  2.新建仓库一：username.github.io  
  （必须为你的github账户的username，而不是昵称啥的）  
  3.新建仓库二，名称随意如vuepress-demo  
  二者的关系是：仓库一负责显示网站内容，我们不需要改动它；日常开发和新增内容，都在仓库二中，并通过 npm run deploy 命令，将代码发布到仓库一  
  4.根目录下新建deploy.sh：
  ```
  #!/usr/bin/env sh

  # 确保脚本抛出遇到的错误
  set -e

  # 生成静态文件
  npm run build

  # 进入生成的文件夹
  cd docs/.vuepress/dist

  # 如果是发布到自定义域名
  # echo 'www.yourwebsite.com' > CNAME
  
  git init
  git add -A
  git commit -m 'deploy'

  # 如果你想要部署到 https://USERNAME.github.io
  git push -f git@github.com:nan-gong/nan-gong.github.io.git master

  # 如果发布到 https://USERNAME.github.io/<REPO>  REPO=github上的项目
  # git push -f git@github.com:USERNAME/<REPO>.git master:gh-pages

  cd -
  ```
  package.json 文件夹中添加发布命令：
  ```
  "scripts": {
    "deploy": "bash deploy.sh"
  }
  ```
  运行npm run deploy