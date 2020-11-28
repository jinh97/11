## webpack配置

### 一般配置

~~~js
const path = require('path')
const htmlWebpackPlugin = require('html-webpack-plugin')
// 导入每次删除文件夹的插件
const cleanWebpackPlugin = require('clean-webpack-plugin')
const webpack = require('webpack')
// 导入抽取CSS的插件
const ExtractTextPlugin = require("extract-text-webpack-plugin")
// 导入压缩CSS的插件
const OptimizeCssAssetsPlugin = require('optimize-css-assets-webpack-plugin')

module.exports = {
  entry: { // 配置入口节点
    app: path.join(__dirname, './src/main.js'),
    vendors1: ['jquery'] // 把要抽离的第三方包的名称，放到这个数组中
  },
  output: {
    path: path.join(__dirname, './dist'),
    filename: 'js/bundle.js'
  },
  plugins: [ // 插件
    new htmlWebpackPlugin({
      template: path.join(__dirname, './src/index.html'),
      filename: 'index.html',
      minify: {
        collapseWhitespace: true, // 合并多余的空格
        removeComments: true, // 移除注释
        removeAttributeQuotes: true // 移除 属性上的双引号
      }
    }),
    new cleanWebpackPlugin(['dist']),
    new webpack.optimize.CommonsChunkPlugin({
      name: 'vendors1', // 指定要抽离的入口名称
      filename: 'js/vendors.js' // 将来再发布的时候，除了会有一个 bundle.js ，还会多一个 vendors.js 的文件，里面存放了所有的第三方包
    }),
    new webpack.optimize.UglifyJsPlugin({
      compress: { // 配置压缩选项
        warnings: false // 移除警告
      }
    }),
    new webpack.optimize.DedupePlugin({ // 设置为产品上线环境，进一步压缩JS代码
      'process.env.NODE_ENV': '"production"'
    }),
    new ExtractTextPlugin("css/styles.css"), // 抽取CSS文件
    new OptimizeCssAssetsPlugin()// 压缩CSS的插件
  ],
  module: {
    rules: [
      {
        test: /\.css$/, use: ExtractTextPlugin.extract({
          fallback: "style-loader",
          use: "css-loader",
          publicPath: '../' // 指定抽取的时候，自动为我们的路径加上 ../ 前缀
        })
      },
      {
        test: /\.scss$/, use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          use: ['css-loader', 'sass-loader'],
          publicPath: '../' // 指定抽取的时候，自动为我们的路径加上 ../ 前缀
        })
      },
      { test: /\.(png|gif|bmp|jpg)$/, use: 'url-loader?limit=5000&name=images/[hash:8]-[name].[ext]' },
      { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ }
    ]
  }
}
~~~

~~~javascript
const path = require('path')
const htmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: path.join(__dirname, './src/main.js'),
  output: {
    path: path.join(__dirname, './dist'),
    filename: 'bundle.js'
  },
  plugins: [ // 插件
    new htmlWebpackPlugin({
      template: path.join(__dirname, './src/index.html'),
      filename: 'index.html'
    })
  ],
  module: {
    rules: [
      { test: /\.css$/, use: ['style-loader', 'css-loader'] },
      { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] },
      { test: /\.(png|gif|bmp|jpg)$/, use: 'url-loader?limit=5000' },
      { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ }
    ]
  }
}
~~~

~~~json
{
  "name": "webpack-senior",
  "version": "1.0.0",
  "description": "",
  "main": "webpack.config.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "webpack-dev-server --open --port 3000 --hot",
    "pub": "webpack --config webpack.pub.config.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "jquery": "^3.2.1"
  },
  "devDependencies": {
    "babel-core": "^6.26.0",
    "babel-loader": "^7.1.2",
    "babel-plugin-transform-runtime": "^6.23.0",
    "babel-preset-env": "^1.6.1",
    "babel-preset-stage-0": "^6.24.1",
    "clean-webpack-plugin": "^0.1.17",
    "css-loader": "^0.28.7",
    "extract-text-webpack-plugin": "^3.0.2",
    "file-loader": "^1.1.5",
    "html-webpack-plugin": "^2.30.1",
    "node-sass": "^4.6.0",
    "optimize-css-assets-webpack-plugin": "^3.2.0",
    "sass-loader": "^6.0.6",
    "style-loader": "^0.19.0",
    "url-loader": "^0.6.2",
    "webpack": "^3.8.1",
    "webpack-dev-server": "^2.9.4"
  }
~~~



