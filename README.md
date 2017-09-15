# express
## 通过node+express写自定义接口(只是get请求的)
1.安装node.
2.安装
npm install express -g
npm install express-generator -g
3.进入项目目入
4.创建项目 express 项目名字
5.安装依赖
6.启动服务器 npm start
首先端口号在bin/wwww ,地址localhost:3000/

现在来创建自定义接口
router
我是在users里改的，如果不想改自己新建一个js再routers文件夹里，再改动app.js
app.use('/', index);
app.use('/users', users);
app.use(你的文件,name);
找到users
``` 
var URL = require('url');
var express = require('express');
var router = express.Router();
/* GET users listing. */
//接口地址localhost:3000/users/getUserInfo?id=1
router.get('/getUserInfo', function(req, res, next) {
    function User() {
        this.name;
        this.city;
        this.age;

    }
    var user = new User();
    var params = URL.parse(req.url, true).query;
    if(params.id == '1') {
        user.name = n;
        user.age = "1";
        user.city = "北京市";

    }else{
        user.name = "SPTING";
        user.age = "1";
        user.city = "杭州市";
    }

    var response = {status:1,data:user};
    res.send(JSON.stringify(response));

});

module.exports = router;
```

改完直接目录下运行 npm start
> api@0.0.0 start H:\express\API
>
> node ./bin/www

表明成功不然就是报错

在本地直接调用这个地址是ok的。
如果想跨域调用的话需要加允许在app.js
```
app.all('*',function (req, res, next) {
    res.header('Access-Control-Allow-Origin', '*');
    res.header('Access-Control-Allow-Headers', 'Content-Type, Content-Length, Authorization, Accept, X-Requested-With , yourHeaderFeild');
    res.header('Access-Control-Allow-Methods', 'PUT, POST, GET, DELETE, OPTIONS');

    if (req.method == 'OPTIONS') {
        res.send(200); /让options请求快速返回/
    }
    else {
        next();
    }
});
```
加完需要重新启动服务器
