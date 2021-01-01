# **常用命令**
|命令|简写|说明|
|:----|:----|:----|:----|:----|:----|
|npm init-y|    |快速生成 package.json文件|
|npm install|npm i|依赖项全部安装|
|npm install --save包名|npm i -S 包名|下载并保存 dependencise 选项|
|npm install --save-dev 包名|npm i -D 包名|下载并保存devDependencise选项|
|npm uninstall 包名|npm un 包名|只删除包,如果有依赖项依然会保存|
|npm uninstall --save 包名|npm un -S 包名|删除的同时也会把依赖信息也去除|

**被墙问题**

|方法一|清除代理|npm config delete proxy<br>npm config delete https-proxy|
|:----|:----|:----|:----|:----|:----|
|方法二|更改代理地址|npm config set registry http://registry.npm.taobao.org|

**npm install -S -D 的区别**

|npm install module_name -S|npm install module_name -D|
|:----|:----|:----|:----|
|npm install module_name --save|npm install module_name --save-dev|
|写入 dependencies|写入 devDependencies|
|是需要发布到生产环境的|里面的插件只用于开发环境，不用于生产环境|
|会在 package.json 的 dependencies 属性下添加 msbuild|会在 package.json 的 devDependencies 属性下添加 msbuild|
|之后运行 npm install --production 或者注明 NODE_ENV 变量值为 production 时，会自动安装 msbuild 到 node_modules 目录中|之后运行 npm install --production 或者注明 NODE_ENV 变量值为 production 时，不会自动安装 msbuild 到 node_modules 目录中|

**查看 npm 配置信息**

npm config list

nrm安装

nrm ls　　// 查看所有的支持源（有*号的表示当前所使用的源,以下[name]表示源的名称）

nrm use [name]　　// 将npm下载源切换成指定的源

# 