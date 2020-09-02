# 面试
## mobx和redux区别
  1.redux状态是只读的，不能直接修改它；mobx状态可变的，可以直接修改  
  2.mobx相对来说状态管理更加简单，学习成本低  
  3.mobx面向对象编程，使用observer绑定状态，观察这个状态，一旦变更就自动更新；redux函数式编程，reducer就是一个存函数，接受输出然后输出新状态，每次都是返回一个新的数据
## vue和react的区别
  vue是mvvm，双向绑定，他监听的是一个数据变化然后去改变ui；
  react是单向数据流，讲求一个函数式编程，一个函数代表一个ui组件，数据不可变。状态变更时，记录新树和旧树的差异，最后把差异更新到真正的dom中
## TCP三次握手
  1、客户端发送syn包到服务器，等待服务器确认接收。2、服务器确认接收syn包并确认客户的syn，并发送回来一个syn+ack的包给客户端。3、客户端确认接收服务器的syn+ack包，并向服务器发送确认包ack，二者相互建立联系后，完成tcp三次握手。四次握手就是中间多了一层 等待服务器再一次响应回复相关数据的过程
## 链判断运算符(Optional Chaining)
  ES2020链判断运算符，使用a?.c?.b代替a && a.c && a.c.b
## 构造函数包含return
  ```
  function A(){
    this.x=3
    return 'ok'; //如果返回基本数据类型，仍然会返回新对象实列
  }
  var b = new A()
  b.x; //3
  ----------------
  function A(){
    this.x=3
    return {x: 4}; //如果返回引用类型（对象、数组、函数），返回值就是return的值
  }
  var b = new A()
  b.x; //4
  ```
## js实现深拷贝的几种方法
  1.使用es6
  ```
  var a=[1,2,3]
  var b=[...a];
  ```
  2.使用concat()方法
  ```
  var a=[1,2,3]
  var c=[];
  var b=c.concat(a);
  ```
  3.使用递归
  ```
  function deep(obj) {
    //判断拷贝的要进行深拷贝的是数组还是对象，是数组的话进行数组拷贝，对象的话进行对象拷贝
    var objClone = Array.isArray(obj) ? [] : {};
    //进行深拷贝的不能为空，并且是对象或者是
    if (obj && typeof obj === "object") {
      for (key in obj) {
        if (obj.hasOwnProperty(key)) {//只遍历自身属性
          if (obj[key] && typeof obj[key] === "object") {
            objClone[key] = deep(obj[key]);
          } else {
            objClone[key] = obj[key];
          }
        }
      }
    }
    return objClone;
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
<!-- <my-btn>11</my-brn> -->
## 常用状态码
  + 1xx（请求处理中）
  + 2xx（请求处理完毕）
      * 200（请求成功）
  + 3xx（重定向）
      * 301（永久重定向）
      * 302（临时重定向）
      * 304（请求资源没有变化，使用缓存）
  + 4xx（客户端请求错误）
      * 400（请求参数错误）
      * 401（没有权限访问，一般表示未登陆）
      * 403（禁止访问，一般表示权限不够，需要更高的权限）
      * 404（请求的资源不存在）
  + 5xx（服务器端错误）
      * 500（服务器内部出错）
      * 503（服务器在维护）
