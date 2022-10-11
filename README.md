# windows环境下使用AList与RaiDrive挂载云盘为本地磁盘

面向对象：1. 比如surface pro的硬盘很小，可以选择这种方法将云盘当硬盘用；2. 可以较快地在各设备端之间进行文件传输；3. 数据、图片视频、游戏大作等实在是太大太多，硬盘确实装不下，直接用网盘。

实际效果：可以用本地装好的软件，打开对应的资源，游戏也可以直接解压玩，同时包括复制、编辑、转移文件，都跟操作本地硬盘一模一样。

![image](https://user-images.githubusercontent.com/48110180/195181196-a0b88844-bc56-437a-8432-1835eca1905b.png)


## AList

https://github.com/alist-org/alist/releases

找到对应的安装版本，以管理员身份运行exe，就直接运行了

![image](https://user-images.githubusercontent.com/48110180/195181303-12284240-c3ee-4be7-b8f0-e5a77c3098eb.png)

这个初始密码，每次都不一样，是随机的

只有一直运行上面这个exe才能打开网页http://127.0.0.1:5244

网页输入这个初始密码登录以进行设置

![image](https://user-images.githubusercontent.com/48110180/195181373-00a79824-021c-4fd5-8c1b-755512ebd0f7.png)

以阿里云盘为例，选定好对应网盘，凭个人喜好命名虚拟路径名，比如：类型：阿里云盘；虚拟路径：Ali

这里第一个重点来了，就是这个令牌：

![image](https://user-images.githubusercontent.com/48110180/195181400-c6d7bb78-650e-45c2-ac3d-69d928c49568.png)

打开以下网址：https://alist-doc.nn.ci/docs/driver/aliyundrive/

![image](https://user-images.githubusercontent.com/48110180/195181476-f2c50441-4205-4546-a03f-ba2fab6eda48.png)

点击Get Token后，在弹出的页面里，用已经登录账号的阿里云盘APP扫码，确认登录后，点击Use AliyunDrive APP To Scan Then Click

等待网页刷新，底下就显示出令牌了：

![image](https://user-images.githubusercontent.com/48110180/195181522-9fc7990f-2ad5-4292-bd4b-62cfcc075846.png)

然后回到需要填写令牌的网页，将这串东西复制进去后，点击右下角保存，这时基本就已经是完成了

我们打开网址：http://127.0.0.1:5244，就能看自己阿里云盘的所有资源了

报错：The input parameter parent_file_id is not valid. for cpp path domain parent_file_id is required

解决方法：网络可能不好，多试着保存几次

阿里云盘的以上操作步骤可能会不太顺利，多试几次就好了

百度网盘的操作同理且步骤很流畅

之后也许会对OneDrive进行挂载


## RaiDrive

https://www.raidrive.com.cn/download

https://github.com/RaiDrive

建议装在C盘以外的其它盘符

如果需要安装环境的话，会要求重启电脑，先重启，再运行一次安装程序

期间会有一个弹窗，选择安装：

![image](https://user-images.githubusercontent.com/48110180/195184957-da054a7b-1dd5-448b-8bf4-a3984bf11824.png)

打开软件，点击这个添加：

![image](https://user-images.githubusercontent.com/48110180/195184974-58445caf-cfcd-42c5-9d3e-c7ad2b438137.png)


第二个重点，按下图所示设置，这里需要特别注意3个参数值：127.0.0.1、5244、/dav。设置好后，点击连接。

![image](https://user-images.githubusercontent.com/48110180/195184996-598e8cc0-839d-4dfb-9f87-06c8ab288922.png)

![image](https://user-images.githubusercontent.com/48110180/195186623-b5aad614-99ee-4981-92d3-fde8eb3e432b.png)

经过上述步骤之后，已经操作完毕。

![image](https://user-images.githubusercontent.com/48110180/195186524-e6b1e779-ae82-4ea3-93c5-9fa8d9d25a54.png)


## AList开机无窗口自启动

这两个软件需要一起开，都不能关，才能挂载。不过可以通过操作做到开机无窗口自启动。

由于AList.exe的版本问题，v2版本可以双击或右键管理员启动，但是v3版本似乎只能cmd启动。

### AList.exe v2（并不能保证这个方法不适用于AList.exe v3）

在AList.exe所在的目录下，创建一个txt文件，将以下代码复制进去，然后将txt另存为alist.bat文件在该目录下

```batch
@echo off
start /min "" "F:\AList\alist-windows-4.0-amd64.exe"
CHOICE /T 5 /C ync /CS /D y /n
taskkill /f /im conhost.exe
```

代码中的F:\AList\alist-windows-4.0-amd64.exe对应于图中的目录，看你exe文件的目录，不同人不一样

创建alist.bat文件的快捷方式，将快捷方式复制或移动到系统启动文件夹即可实现开机无窗口自启动。

Windows系统都有一个“启动”文件夹，把需要打开的程序的快捷方式或脚本放到“启动”文件夹里，就可以实现开机自启动。启动”文件夹分为两种：“系统启动文件夹”和“用户启动文件夹”。

系统启动文件夹：

Win10系统“启动”文件夹的路径为： *X:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp*(注：X为Win系统盘盘符)

如果想要实现应用程序在所有的用户登录系统后都能自动启动，就把该应用程序的快捷方式放到“系统启动文件夹”里；

cmd中打开“系统启动文件夹”的命令  shell:Common Startup  或者 %programdata%\Microsoft\Windows\Start Menu\Programs\Startup

用户启动文件夹：

Win某个用户的“启动”文件夹路径为：*X:\Users\用户名\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup*，

如果想要实现某个应用程序只在某个用户登录系统时自动启动，那么就把该应用程序的快捷方式放到这个用户的“启动”文件夹里。

cmd中打开“用户启动文件夹”的命令  shell:startup

由于电脑本身配置的问题，可能出现RaiDrive先运行的情况，导致RaiDrive出现报错说“服务器积极拒绝”。多等一会儿，等bat文件运行完毕，这个报错就会解决。同时如果马上打开阿里网盘，可能会出现空白文件夹的情况，这个也是等一会儿就好了，但是百度网盘就不会有这种情况。

### AList.exe v3（并不能保证这个方法不适用于AList.exe v2）

在AList.exe所在的目录下，创建一个txt文件，将以下代码复制进去，然后将txt另存为alist.vbs文件在该目录下

```batch
Set ws = CreateObject("Wscript.Shell") 
ws.run "cmd /c F:/AList/alist-windows-4.0-amd64.exe",vbhide
```

创建alist.vbs文件的快捷方式，将快捷方式复制或移动到系统启动文件夹即可实现开机无窗口自启动。

## 关于手机访问的问题

（未验证）在手机上安装一个nPlayer，即可在手机上看资源。

## 更换磁盘图标

觉得原来的图标丑的话，可以用软件或者自己手动改。

![image](https://user-images.githubusercontent.com/48110180/195192682-41e3e40e-7028-4ec3-8a51-1a926ec45aff.png)


