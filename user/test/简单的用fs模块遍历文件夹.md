# 讲一些没用的东西
为什么写了这个博客呢，因为最近遇到需要返回目录文件的功能，这里就用nodejs实现下

# 需要模块
* fs
* path

# 代码
```
var fs = require('fs');
var path = require('path');
function findfile(userid,callback){
  var fname = {
    author : userid,
    title : new Array()
  };
  var needfind = '../user/' + userid ;
  function indexfile( inputPath){
       let files = fs.readdirSync(inputPath)      //同步读取文件
       for(file of files){
           let filePath = inputPath + '/' + file;   //获取文件路径
           let fileState = fs.statSync(filePath);
           if(fileState.isDirectory()){          // 如果是目录 递归
               indexfile(filePath)
           }else{
               fname.title.push(file.slice(0,file.length-3));     //字符串截取，去掉文件后缀
           }
       }

  }
  indexfile(needfind)
  callback(fname);
}


exports.findfile = findfile;
```
写的是一个node模块主要是遍历指定用户目录，将目录下所有文件推入数组返回



封面画师：[Yuu]

[Yuu]:https://www.pixiv.net/member.php?id=3137712
