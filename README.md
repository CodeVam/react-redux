### 全局安装[Express](http://www.expressjs.com.cn/)
```bash
npm install -g express
```
### 配置express框架
1. 在项目目录使用express命令生成Express框架
```bash
express --view=ejs
```
1. ejs为模板引擎，如需更换自行设置，比如[artTemplate](https://github.com/aui/artTemplate)
- 安装artTemplate
```bash
npm install art-template express-art-template
```
- 配置express
```javascript
//删除ejs引擎
//app.set('view engine', 'ejs');
//注册新的模板引擎
app.engine(“art”,require(“express-art-template”));
app.set(“view engine”,art);
```
2. 安装Express依赖包
```bash
npm install
```
### 安装[react](https://facebook.github.io/react/docs/hello-world.html)
```bash
npm install -S react react-dom
```
### 安装[webpack](https://doc.webpack-china.org/)
```bash
npm install -D webpack
```
##### 编译jsx
```bash
npm install -D babel-core babel-loader babel-preset-es2015 babel-preset-stage-3 babel-preset-react
```
##### 模块化css
```bash
npm install -D node-sass
```
##### 编译sass
```bash
npm install -D sass-loader postcss-loader css-loader style-loader
```
##### 图片处理
```bash
npm install -D file-loader url-loader
```
### 热替换与自动刷新
##### webpack-dev-server
```bash
npm install -D react-hot-loader webpack-dev-server
```
```javascript
module.exports = {
    entry: [
      'react-hot-loader/patch',
       // 开启react代码的模块热替换（HMR）

      'webpack-dev-server/client?http://localhost:8080',
       // 为webpack-dev-server的环境打包好运行代码
       // 然后连接到指定服务器域名与端口
       'webpack/hot/only-dev-server',
       './index.jsx'
    ],
    devServer: {
        hot: true,
        // 开启服务器的模块热替换（HMR）

        contentBase: resolve(__dirname, 'dist'),
        // 输出文件的路径

        publicPath: '/'
        // 和上文output的"publicPath"值保持一致
    },
    plugins: [
        new webpack.HotModuleReplacementPlugin(),
        // 开启全局的模块热替换（HMR）

        new webpack.NamedModulesPlugin(),
        // 当模块热替换（HMR）时在浏览器控制台输出对用户更友好的模块名字信息
      ],
}
```
##### webpack-dev-middleware
```bash
npm install -D webpack-dev-middleware webpack-hot-middleware
```
```javascript
onst webpack = require('webpack');
const path = require('path');

const ROOT_NAME = process.env.ROOT_NAME||"";

var hotMiddlewareScript = 'webpack-hot-middleware/client?path=/__webpack_hmr&timeout=20000';
const config = {
  context: path.resolve(__dirname,'./src'),
  devtool: "cheap-eval-source-map",
  entry: {
    index: [
      hotMiddlewareScript,
      './index.jsx',
    ],
    vender: ['react', 'react-dom']
  },
  output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname,'public'),
    publicPath: "/public/"
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /(node_modules|bower_components)/,
        use: {
          loader: 'babel-loader'
        }
      },
      {
        test: /\.scss$/,
        include: /scss/,
        use: [{
          loader: "style-loader"
        }, {
          loader: "css-loader",
          options: {
            sourceMap: true
          }
        }, {
          loader: 'postcss-loader'
        }, {
          loader: "sass-loader",
          options: {
            sourceMap: true
          }
        }]
      }
    ]
  },
  plugins: [
    new webpack.HotModuleReplacementPlugin(),
    new webpack.NamedModulesPlugin(),
  ]
};


module.exports = config;
```
```javascript
var webpack = require("webpack");
var webpackConfig = require("./webpack.config.dev");
var compiler = webpack(webpackConfig);

var webpackDevMiddleware = require("webpack-dev-middleware");
var webpackHotMiddleware = require('webpack-hot-middleware');

app.use(webpackDevMiddleware(compiler, {
  publicPath: webpackConfig.output.publicPath,
  stats: { colors: true }
}));

app.use(webpackHotMiddleware(compiler));
```
### 路由组件
```bash
npm install -S react-router-dom
```
### 全局状态管理
```bash
npm install -S redux
```
### 状态与React结合
```bash
npm install -S react-redux
```
### 路由与Redux结合
```bash
npm install -S react-router-redux
```
基础的配置与打包基本就有了，如需其他功能插件可自行导入
