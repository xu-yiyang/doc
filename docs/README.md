# js，css小效果集合
  ## 浏览器数据库存储
  参考：http://www.cnblogs.com/xiaowei0705/archive/2011/04/19/2021372.html  
  存储：sessionStorage.setItem('变量名','值');  
  读取：var a=sessionStorage.getItem('变量名')  
  ## json格式转换
  JSON.stringify() //数据转字符串  
  JSON.parse() //字符串转对象数组  
  ## 替换手机号中间4位为*号
  dataSelector.mobile.replace(/(\d{3})\d{4}(\d{4})/, '$1****$2')  
  ## 鼠标移入移出，如果标签中有子元素不会重复触发
  onMouseEnter   onMouseLeave
  ## 鼠标移入移出，如果标签中有子元素会重复触发
  onmouseover   onmouseout
  ## 文字溢出隐藏省略号
  overflow: hidden;text-overflow: ellipsis;white-space: nowrap;
  ## 实现0.5边框宽度
  <http://www.cnblogs.com/PeunZhang/p/4709822.html>
  ## 模块两端对齐
  <http://www.cnblogs.com/PeunZhang/p/3289493.html>
  ## 使页面元素变为可编辑
  ```
  document.designMode="on";
  <p contenteditable="true">是一个帅哥</p><p contenteditable="true">是一个帅哥</p>
  ```
  ## 延迟几秒自动跳转到该页面
  window.setTimeout("window.location='index.shtml'",5000);
  
  ## 单选多选点击css事件
  input[type="checkbox"]:checked{}
  ## 判断多选是否选中
  $(this).is(':checked')==true
  ## 判断元素是否隐藏
  if(!$(".dialog-overlay2").is(":hidden"));
  ## 多选框全选
  ```
  $(".j-check-all").click( 
      function(){ 
        if(this.checked){ 
        $("input[name='checkname']").each(function(){this.checked=true;}); 
        }else{ 
        $("input[name='checkname']").each(function(){this.checked=false;}); 
        } 
      } 
  );
  ```
  ## css使用after获取元素属性
  ```
  <h2 data-text="天赐美妞">天赐美妞</h2>
  .text-gradient[data-text]::after {  
    content: attr(data-text);  
  }
  ```
  ## ios弹性滚动
  -webkit-overflow-scrolling: touch;
 ## 实现在一个页面展示多个swiper轮播图的功能
  ```
  $(".swiper-container").each(function(){
    $(this).swiper({
      loop: true,
      initialSlide :0,
      pagination:$('.swiper-pagination',this),
      nextButton: $('.arrow-right',this),
      prevButton:$('.arrow-left',this)
    });
  });
  ```
  <http://blog.csdn.net/amyliyanice/article/details/59483499>
  ## 雪碧图移动端背景图定位公式
  .box_left{ left:0px; background-position:0px 59.1729%;/*背景定位值是：背景图标所在图的位置/(背景图片高度-容器高度)*/ }
  ## 百分比宽度构造正方形
  width: 13%; height: 0px; padding-bottom: 13%; 或 width: 8vw; height: 8vw; 
  ## 发送qq网站出现图片介绍
  ```
  <div style='margin:0 auto;width:0px;height:0px;overflow:hidden;'>     
    <img src="images/UI主图.jpg" width='800' height="800">
  </div>
  ```
  ## 只能输入数字
  ```
  <input onKeypress="return (/[\d]/.test(String.fromCharCode(event.keyCode)))" maxlength="11">
  
  <input type="text" onkeyup="value=value.replace(/[^\d]/g,'') " ng-pattern="/[^a-zA-Z]/" />
  ```
  ## 只能输入数字和限制几位数
  ```
  <input type="number" id="code" value="" placeholder="请输入短信验证码">
  let codeDom = document.getElementById('code')
  var codeValue = ''
  codeDom.oninput = function () {
    if (codeDom.value !== '') {
      codeValue = codeDom.value
    } else if (codeValue.length === 1) {
      codeValue = ''
    }
    codeDom.value = codeValue.replace(/[^\d]/g, '').slice(0, 6)
  }
  ```
  ## nth-child公式
  an+b-----a表示有几种循环样式，b表示循环中的第几个，如:3种样式要循环，a=3,b=1,b=2,b=3
  ## 取消伪类before和after
  设置contrnt:none
  ## 两端对齐
  :after{display:inline-block;content:'';width:100%;}
  ## 返回顶部
  $(".return").click(function(){
      $('body,html').animate({scrollTop:0},200);
  });
  ## 媒体查询
  ```
  @media screen and (max-width:320px){body {font-size:62.5%!important;}}

  @media screen and (min-width:320px){body {font-size:62.5%!important;}}

  @media screen and (min-width:360px){body {font-size:70.3%!important;}}

  @media screen and (min-width:400px){body {font-size:78.1%!important;}}

  @media screen and (min-width:440px){body {font-size:85.9%!important;}}

  @media screen and (min-width:460px){body {font-size:89.9%!important;}}

  @media screen and (min-width:480px){body {font-size:93.8%!important;}}

  @media screen and (min-width:540px){body {font-size:105.5%!important;}}

  @media screen and (min-width:560px){body {font-size:109.4%!important;}}

  @media screen and (min-width:640px){body {font-size:125%!important;}}
  ```
  ## 禁止表单获取光标后页面放大的问题
  ```
  <meta name="apple-mobile-web-app-capable" content="yes">  
  <meta name="viewport" content="width=device-width, initial-scale=1.0,minimum-scale=1.0, maximum-scale=1.0, user-scalable=no">
  ```
  ## 获取最后一个“-”符号位置，截取字符串到最后一个“-”符号为止
  ```
  var txt="asd-czx-asd-aw";
  var txtIndex=$(this).parents("label").siblings('.layer-name').text().lastIndexOf("-");
  if (txtIndex != -1) { 
  console.log(txt.substr(0,txtIndex));//asd-czx-asd
  }
  ```
  ## echarts图标渐变色设置
  ```
  areaStyle: {normal: {
    color: new echarts.graphic.LinearGradient(1, 0, 0, 0, [{
          offset: 0,
          color: 'rgba(0, 0, 0, 1)'
      }, {
          offset: 0.5,
          color: 'rgba(255, 255, 111, 1)'
      }, {
          offset: 1,
          color: 'rgba(28, 159, 255, 1)'
      }])
  }},
  ```
  ## 更改选中文本的样式
  ```
  ::selection
  {
    color: white;
    background-color: red;
  }
  
  ::-moz-selection  /* Firefox needs an extra attention for this */
  {
    color: white;
    background-color: red;
  }
  ```
  ## 垂直居中
  ```
    方法1：
    .Absolute-Center {
      position: absolute;margin: auto;top: 0; left: 0; bottom: 0; right: 0;
    }

    方法2：
    .vc{
        position: relative;
        top: 50%;
        transform: translateY(-50%);
        -webkit-transform: translateY(-50%);
        -o-transform: translateY(-50%);
    }
  ```
  ## iframe交互
  ```
  找到最上层的标签：$("想找的标签",top.window.document)
  {原生：window.parent或jq:$(".close-icon",parent.document)}  iframe页面调用父页面对象

  父页面页面调用iframe对象
  $('iframe的ID').contents().find("要获取的元素").addClass("srtdl");
  ```

