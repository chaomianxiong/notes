mongodb 安装配置

版本：mongodb-win32-x86_64-2008plus-ssl-3.6.21-signed.msi

不用4.xx.xx 版本原因：官网上下载不了 msi 格式的，并且 4.xx 版本需要公钥 

下载地址：http://dl.mongodb.org/dl/win32/x86_64

安装过程中不要勾选 Install MongoDB Compass 。这是一个图形化软件

配置环境变量  在电脑中找到环境配置 将 mongodb 的安装文件夹路径配置进去

在 D 盘根目录建立 data 文件夹 ，在 data 文件夹下建立 db 文件夹

在 mongodb  安装目录下运行 mongod.exe 程序(启动服务器)

在 mongodb  安装目录下运行 mongo.exe 程序(连接服务器)  在cmd 中出现 > ,说明连接成功了