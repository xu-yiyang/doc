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