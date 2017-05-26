## React中key的作用

  React是利用虚拟dom对页面上的元素进行管理，当有多个重复元素时，react无法快速标识一个元素节点，导致react在做diff算法时不能重用只改变位置的元素，而是重新创建一个新元素，效率会低很多。所以react通过在这样的元素中加入属性key来唯一标识当前的元素节点，以便在以后的diff中去尽可能重用元素节点以提升效率。

## createElement与cloneElement的区别

  1. 作用不同: createElement依据一些给定的属性特征创建新的react元素;cloneElement是依据已经存在的react元素创建新的元素，并保留被克隆元素的所有属性，同样也可以添加自身的新属性。
  2. 使用不同: createElement和cloneElement的后两个参数相同，第一个参数不同:createElement的第一个参数必须是字符串(string类型,如'li','div'等)或者ReactClass创造的类;cloneElement的第一个参数必须是ReactElement类型。

## React-Native的优缺点

  1. 优点:
    * 使用相同的jsx语法编写两套代码，开发效率较高
    * 使用弹性盒子布局完成自适应布局，简单高效
    * 更贴近原生开发
  2. 缺点:
    * 编写难度大于web技术，需要懂一些原生的扩展
    * 扩展性低于web，功能实现低于原生
    * 不同平台可能需要多套代码
    * ui组件不全

## React-Native相对于原生的ios和Android的优势

  * React-Native是使用jsx语法开发，对原生的语法要求低，对人员的要求就低
  * 开发效率高于原生
  * 后期对产品的维护成本低于原生

## React-Native的调试方法

  * 使用Chrome浏览器进行调试:将应用设置为在模拟器中运行，Command+D，选择Debug in Chrome
  * 在控制台中访问日志调试:在运行RN应用时，输入命令react-native log-ios(或者log-android)
  * 在应用内通过提示调试:红屏为报错，手动设置console.error();黄屏为警告，手动设置console.warn()
  * 安装react-devtools并启用react-devtools调试

## redux中的store对象

  store是将action和reducer联系在一起的对象。事件触发action，传递信息到store对象中，触发reducer来根据信息的不同改变state到新的state，最后引起render函数重新渲染视图的展示。store以action为输入，以reducer为引擎处理信息，最后以新state为输出。

## 项目中负责的工作内容

  * 负责的板块: 用户提问板块
  * 板块的组成: 前端页面，异步交互，后台代码
  * 内容:
    1. 前端页面: 采用react + material-ui + react-quill组件通过webpack打包生成js文件插入到ejs模板页面，动态生成页面主体。主要利用react状态state对应界面的思想来管理页面视图，以达到不同界面之间的便捷切换;使用material-ui能快速搭建各种效果的页面，提升用户体验;而react-quill主要提供原生react编写的富文本编辑器，满足用户对问题内容的编写。
    2. 异步交互: 本项目采用ejs模板引擎，但页面主体内容是通过react组件渲染，所以采用异步请求数据和提交数据的方式完成前后端的交互任务，提问界面则主要是对登录用户的信息和问题分类的请求，以及对问题内容的提交。这里采用react支持的fetch函数来完成异步交互。
    3. 后台代码: 本项目后台采用node.js的express + mongodb搭建。对于提问板块:
      * 需要自己编写:　问题提交请求的处理，合法问题写入问题数据库过程，用户信息的更新
      * 需要调用其他接口:　登录用户的信息，所有的分类信息
      * 需要使用的数据库: 用户集合(users)，问题集合(questions)
  * 注意事项:
    1. material-ui的组件需要提供主题才会正确显示，在组件上添加事件时需要安装react-tap-event-plugin才会生效
    2. fetch函数在react中可以直接使用，分为GET和POST请求两种，默认情况下不会在请求中携带cookie信息，如果需要验证用户信息则必须携带cookie信息，则需要设置credentials: 'include'
    3. 事件绑定的处理函数容易存在this的绑定问题，需要将this指向当前的组件自身，处理主要两种:
      * 使用es6的箭头函数:
      ```
      onTouchTap = { () => { this.callback() } }
      ```
      * 使用bind函数绑定:
      ```
      onTouchTap = { this.callback.bind(this) }
      ```
    * 项目的不足:
      1. 用户体验把握准:对于悬赏时间和悬赏金的填写方式存在争议。
        * 滑动选值:只要考虑用户的提问可以快速选值，不足在于需要滑动来调整到用户想要的值
        * 输入框:用户可以直接输入向要设置的值，不足在于需要使用键盘操作以及需要对值做一些规范化的处理

      2. 在编写node是需要修改三个数据集合的数据，业务处理在嵌套在回调函数中。处理的方式:
        * 由于回调业务逻辑简单就直接通过回调的嵌套来完成
        * npm来安装async或者bluebird模块完成业务处理的流程化，避免回调的嵌套过多造成理解和维护困难
