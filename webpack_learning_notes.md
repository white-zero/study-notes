* 根目录new一个webpack.config.js
* js 文件打包(react语法的处理)
    ```
    entry: './src/app.jsx',
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: "app.js"
    },
    ```


* html 文件打包
    - const HtmlWebpackPlugin = require('html-webpack-plugin')
    ```
    plugins: [
        new HtmlWebpackPlugin({
            template: './src/index.html'
        })
    ]
    ```

    //temlate是模版。即待打包的html文件


* css 文件打包
    - tips: 要在js文件里import


    ```
    {
         test: /\.css$/,
         use: [
                    'style-loader',
                    'css-loader'
                ]
    ```

    - const ExtractTextPlugin = require('extract-text-webpack-plugin')
            （这个插件可以在打包的文件中，把css独立出来，可以提前加载）代码改为

    ```
    {
    test: /\.css$/,
    use: ExtractTextPlugin.extract({
         fallback: "style-loader",
         use: "css-loader"
               })
    }
    ```



    ```
    plugins: [
        new HtmlWebpackPlugin({
            template: './src/index.html'
        }),
        new ExtractTextPlugin("index.css")
    ]
    ```


* sass文件的处理  (一种CSS的开发工具，提供了许多便利的写法，大大节省了设计者的时间，使得CSS的开发，变得简单和可维护。)
    - 要同时下载
             "sass-loader": "^6.0.6",
             "node-sass": "^4.14.1"


    ```
    {
       test: /\.scss$/,
       use: ExtractTextPlugin.extract({
       fallback: 'style-loader',
       use: ['css-loader', 'sass-loader']
          })
    },
    ```

* 图片的打包
    - 下载 url-loader@0.6.2  file-loader@1.1.6

    ```
    {
    test: /\.(png|jpg|gif)$/,
    use: [
       {
          loader: "url-loader",
          options: {
                limit: 8192
                        }
                    }
      ]
    }
    ```

* 字体图标的配置（npm install font-awesome）

    - 现在js文件中引入 font-awesome/css/font-awesome.min.css

    - 再在webpack.config.js里配置
        ```
    {
     test: /\.(eot|svg|ttf|woff|woff2|otf)$/,
      use: [
              {
            loader: 'url-loader',
            options: {
                limit: 8192
                    }
              }
        ]
    }
    ```

* 提出公共模块
    - 先 const webpack = require('webpack')


    ```
    plugins: [
        new HtmlWebpackPlugin({
            template: './src/index.html'
        }),
        new ExtractTextPlugin("css/[name].css"),
        new webpack.optimize.CommonsChunkPlugin({
            name : 'common',
            filename: 'js/base.js'
        })
    ]
    ```

* webpack-dev-server(页面自动更新，挂载在自定义的端口上)
    - 修改端口

    ```
    devServer: {
        port: 8086,
    }
    ```

    - 在output里加publicPath：“/dist/”  (当报错一些字体文件找不到的时候加。)
    - 终端 node_modules/.bin/webpack-dev-server 启动
    - 在package.json里加几个scripts 里的字段

    ```
    "dev": "node_modules/.bin/webpack-dev-server",
    "dist": "node_modules/.bin/webpack -p"    //线上环境时，最好后面加上-p
    ```
    
    ---


    "babel-core": "^6.26.0",
    "babel-loader": "^7.1.2",
    "babel-preset-env": "^1.6.1",
    "babel-preset-react": "^6.24.1",
    "css-loader": "^0.28.8",
    "extract-text-webpack-plugin": "^3.0.2",
    "html-webpack-plugin": "^2.30.1",
    "react": "^16.2.0",
    "react-dom": "^16.2.0",
    "react-scripts": "3.4.1",
    "style-loader": "^0.19.1",
    "webpack": "^3.10.0"
    "sass-loader": "^6.0.6",
    "node-sass": "^4.14.1"
    “font-awesome": "^4.7.0",
    "webpack-dev-server": "^2.9.7",


----------------------------------------
