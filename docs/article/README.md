# 插件类使用总结
## ali-oss
  功能: 可以将文件资料上传到阿里云的oss
  实现，以react为例：
  ```
    yarn add ali-oss
    import OSS from 'ali-oss'
    const client = new OSS({   
      accessKeyId: '',  // 后端提供
      accessKeySecret: '',    // 后端提供 
      stsToken: '',  // 后端提供
      bucket: 'media-cash-market-in', // oss目录
      region: 'oss-ap-southeast-5', // 所在地区，可去https://www.alibabacloud.com/help/zh/doc-detail/31837.html查询
    });
    <input type="file" name='face' accept="image/*" onChange={e => {
      change(e)
    }}/>
    const change = (e) => {
      const target = e.target
      if (target?.files?.[0]) {
        Toast.loading('Menuat, tidak ada konten...', 0);
        const file = target.files[0];
        const windowURL = window.URL || window.webkitURL;
        const dataURL = windowURL.createObjectURL(file);
        
        const reader = new FileReader();//此处主要用FileReader处理         
        reader.readAsDataURL(file);               
        reader.onloadend = () => {  
          const index1 = file.name.lastIndexOf('.');
          const index2 = file.name.length;
          let fileName = file.name.substring(0, index1); // 文件名
          const suffix = file.name.substring(index1, index2); // 后缀名
          // fileName = this.stripscript(fileName);
          const url = fileName + '_' + new Date().getTime() + suffix; 
          //oss上传
          client.put(
            'loan_user/' + url,   //放到loan_user文件夹下                  
            file,
          ).then(res => {
          })
        }
      }
    }
  ```
## 怎么部署git项目
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