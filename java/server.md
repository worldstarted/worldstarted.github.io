# 搭建服务器

1. 安装nginx

2. 安装tomcat

   ```sh
   sudo apt-get install tomcat9-admin
   sudo apt-get install tomcat9
   
   #使用下面命令我们可以查找到tomcat的相关路径
   sudo find / -name *tomcat*
   
   
   #打开tomcat的bin目录
   cd /usr/share/tomcat9/bin
   
   #启动tomcat的服务
   sudo ./startup.sh
   # 如果报错，可能需要手动创建logs文件夹
   ```

   

## vim技巧

> 注释多行：
>
> 1）将光标置于第一行要注释的地方， 按下Ctrl-V(or CtrlQ for gVim)进入VISUAL BLOCK模式，移动光标选中所有所需注释的行；
>
> 2）依次按下大写`I(shift+i)，``#，`Esc, vim会在所选行的每行行首添加`#。`
>
> **对于debian/ubuntu默认使用的vim版本，上述方法不起作用。**需将第2步改为，输入 : `，出现:'<,'>提示符后输入s/^/#`
>
> 取消多行注释：
>
> 将光标置于第一个 `#` 处， 按下Ctrl-V ，移动光标选中所有需要取消注释的行，按x，所有行首的#会被删除。