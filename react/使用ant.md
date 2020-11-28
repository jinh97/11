# ant使用

安装

~~~
yarn add antd
~~~

示例

~~~
import { DatePicker } from 'antd';
ReactDOM.render(<DatePicker />, mountNode);
~~~

样式导入

~~~
import 'antd/dist/antd.css'; // or 'antd/dist/antd.less'
~~~

按需导入----4.0

`antd` 的 JS 代码默认支持基于 ES modules 的 tree shaking。 

按需加载---4.0之前

> 注意：antd 默认支持基于 ES module 的 tree shaking，不使用以下插件也会有按需加载的效果。

下面两种方式都可以只加载用到的组件。

- 使用 [babel-plugin-import](https://github.com/ant-design/babel-plugin-import)（推荐）。

  ```
  // .babelrc or babel-loader option
  {
    "plugins": [
      ["import", {
        "libraryName": "antd",
        "libraryDirectory": "es",
        "style": "css" // `style: true` 会加载 less 文件
      }]
    ]
  }
  ```

  然后只需从 antd 引入模块即可，无需单独引入样式。等同于下面手动引入的方式。

  ```
  // babel-plugin-import 会帮助你加载 JS 和 CSS
  import { DatePicker } from 'antd';
  ```

- 手动引入

  ```
  import DatePicker from 'antd/es/date-picker'; // 加载 JS
  import 'antd/es/date-picker/style/css'; // 加载 CSS
  // import 'antd/es/date-picker/style';         // 加载 LESS
  ```



