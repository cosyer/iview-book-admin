# 功能介绍
	1.分类管理
	2.出版管理
	3.读者管理
	4.图书管理
	5.借阅管理
	6.借阅记录
	7.图书概览
	另外还有主题功能，有多个主题可供选择(主题代码被我注释了，在store/modules/menu.js下) 
	可以全屏放大缩小
## 技术栈
```js
    // 前端
    1.vue
    2.vue-router
    3.vuex
    4.iview
    5.axios

    // 后端
    1.Node
    2.Eggjs
    3.Mongodb + Mongoose
```

## 安装
```js
    $ git clone  https://github.com/cosyer/iview-book-admin.git
    $ cd iview-book-admin
    // 前端
    $ npm i
    $ npm run dev
    // 打开地址 http://127.0.0.1:9898


    // 后端  
    // 确认已经安装mongodb  这里默认配置是 
    // config.mongoose = {
    //     url: 'mongodb://127.0.0.1:27017/book',
    //     options: {},
    // };

    // 数据库需要插入一条初始admin的数据
    //   db.users.insert({
    //       "userName":"admin",
    //       "password":"admin",
    //       "isAdmin": true
    //   })
    $ cd server
    $ npm i 
    $ npm run dev
    
    // 打开地址 http://127.0.0.1:7001/public/web/index.html
```
   
 ## 参考
 iView GitHub：https://github.com/iview/iview
 iView Admin GitHub：https://github.com/iview/iview-admin
