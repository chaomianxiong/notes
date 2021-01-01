把Typora添加到右键菜单

更新于2020-12-31

---

1、打开注册表

![](E:\notes\Pictures\Tools\把Typora添加到右键菜单\1-打开注册表.png)

2、定位
HKEY_CLASSES_ROOT\Directory\Background\shell

![](E:\notes\Pictures\Tools\把Typora添加到右键菜单\2-定位.png)

3、新建项Typora
更改默认数据为Typora，再新建一个新建字符串值，命名为icon,其数据改为Typroa的安装路径

![](E:\notes\Pictures\Tools\把Typora添加到右键菜单\3-新建项typora.png)

4、右键Typora新建项command,
双击右边窗口的默认文件，填写文件路径,路径中的双引号不能少，表示字符串。

![](E:\notes\Pictures\Tools\把Typora添加到右键菜单\4-新建项command.png)

5、效果

![](E:\notes\Pictures\Tools\把Typora添加到右键菜单\5-效果图..png)