## nodejs的模块机制

每一个js文件都是一个单独的模块，拥有自己的作用域
可以通过以下方式加载模块
```js
require('./test.js');
```

> 需要注意这里的路径问题：  
> 模块加载的路径查找顺序：  
> 绝对路径>  
> ./xx.js 相对路径  
> xx.js       这样的写法会去查找nodejs的核心模块或者node_modules文件夹里面的模块, 而不会查找相对路径，因此这里要注意写法  
> 查找规则：  
> 1.首先会安装加载模块的文件名进行查找  
> 2.如果没有找到，会在加载模块后面添加.js文件继续查找  
> 3.如果还没有找到，则会在文件名称后加上.json继续查找  
> 4.如果还没，则会在文件名称后加上.node继续查找

在一个文件中使用var定义的变量，其作用域就是当前文件所在的独立模块，不能被其他的模块访问，若想要访问其他模块的变量和方法，可以通过以下方法
1. 将属性或者方法通过global的方式定义, 但是这种方式并不推荐

    ```js
    global.a = 100;
    global.pers = function();
    ```

2. 使用模块对象module.exports 或者 exports
    ```js
    var a = 100;
    exports.a = a;
    ```

    ```js
    var mm = require(./xx.js);
    console.log(mm.a);
    ```