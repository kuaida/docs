# 我需要完成的功能
  * 完成忘记密码部分

# 我的主要操作文件
  * routes/resetPasswd.js
  * components/resetPasswd.js
  * views/resetPasswd.ejs

## 2017.5.25
  * 完成前端页面
  * 正在进行和后端的交互操作
  * 注册了一个新浪邮箱，用于发送验证码，验证用户邮箱信息。
    * 账号:ikuaida
    * 密码:ikda.cc
  * 引入一个库nodemailer 作用邮箱发送数据

## 2017.5.23
  * webpack.congfig.js文件加入
  ```js
    resetPasswd:'./components/resetPasswd.js'
  ```
  * app.js加入
  ```js
    var resetPasswd = require('./routes/resetPasswd');
    app.use('/resetPasswd', resetPasswd);
  ```
  * routes加入resetPasswd.js文件

  * components加入resetPasswd.js文件
    * 使用material-ui
      ```js
      //监听触摸/点击/点击事件的依赖组件
      import injectTapEventPlugin from 'react-tap-event-plugin';
      injectTapEventPlugin();
      //material-ui的光明主题
      import MuiThemeProvider from 'material-ui/styles/MuiThemeProvider';
      import getMuiTheme from 'material-ui/styles/getMuiTheme';
      //自定义主体　palette设置主体颜色
      const muiTheme = getMuiTheme({
        palette: {
          primary1Color: deepPurple900,
        }
      });
      ...
      //一定要把主体把内容包住
      <MuiThemeProvider muiTheme = { muiTheme }>
        <HorizontalTransition />
      </MuiThemeProvider>
      ```

  * views加入resetPasswd.ejs文件
