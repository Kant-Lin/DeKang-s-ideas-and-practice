# Github+Typora计划操作日志

根据搜索结果，采用方案如下。本文将以方案+标注的形式进行操作，每一步操作以及网址皆附在备注当中。

## 前言

gitbook在2018年4月9日发布了新的版本v2。新的版本官网已经变成 www.gitbook.com ，旧的平台地址为 legacy.gitbook.com ，已经不能再新注册了，并且新旧平台的数据都不互通。最大的区别是旧版是把每本书作为一个 Git Repository 来进行版本管理，是book的概念；但是新版则升级为 Orgnization，然后再在这个 Orgnization 里面创建一个 Space（旧版叫 Book）。

个人还是喜欢旧版的排版方式。但旧版已经不能再注册了。同时gitbook editor也是不能登陆了，这一点让我纠结了很久，后来才发现是新旧版本的问题，才有了这个教程。

此教程是使用typora来编写markdown，所见所得，非常方便；然后再使用git将写的文章推送到github上，最后在gitbook上面设置关联，这样就完成了。

全部软件下载位置：https://pan.8994.cn:5001/sharing/uWeIGwijE ，密码: git

## 安装gitbook命令

因为 GitBook 是基于 Node.js，所以我们首先需要安装 Node.js（下载地址：https://nodejs.org/en/download/ ），找到对应平台的版本安装即可。安装完成之后，需要重启电脑，之后再运行`npm install -g gitbook-cli`。

再使用`gitbook -V`来查看是否有正常安装成功了。

```
C:\Users\fdm>npm install -g gitbook-cli
C:\Users\fdm\AppData\Roaming\npm\gitbook -> C:\Users\fdm\AppData\Roaming\npm\node_modules\gitbook-cli\bin\gitbook.js
+ gitbook-cli@2.3.2
added 578 packages from 672 contributors in 45.615s

C:\Users\fdm>gitbook -V
CLI version: 2.3.2
GitBook version: 3.2.3
```

> 安装Node.js，若使用自带下载器下载，速度极其慢。复制链接到迅雷则迅速下完（有会员真好）
>
> 安装过程里，除了点一下同意协议，其他全都无脑点下一步即可。安装完成之后，打开node.js的安装路径，复制地址，如：C:\Program Files\nodejs\，然后右键【我的电脑】-【属性】-【高级系统设置】-【环境变量】-【系统变量】-【Path】-【编辑】-【新建】，把地址粘贴进去。（如果已经添加就算了）
>
> 之后打开Node.js 进行安装，但是输入`npm install -g gitbook-cli` 之后报错，代码为：**npm should be run outside of the node repl, in your normal shell.** 解决办法为，改为Node.js Command Prompt 这个软件，输入`npm install -g gitbook-cli` ，即可开始安装。
>
> 但此时又出现报错：**[..................] / fetchMetadata: sill resolveWithNewModule gitbook-cli@2.3.2 checking installab……** 
>
> 解决办法为：重启该软件，输入sudo npm cache clean，回车；再输入npm config set registry https://registry.npm.taobao.org，回车即可解决。
>
> 安装完成之后，一定要输入gitbook -V 检查安装版本。因为这一步还有可能出问题：
>
> ```
> [root@pes nodejs]# gitbook -V
> CLI version: 2.3.2
> Installing GitBook 3.2.3
> /data/soft/nodejs/lib/node_modules/gitbook-cli/node_modules/npm/node_modules/graceful-fs/polyfills.js:287
>       if (cb) cb.apply(this, arguments)
>                  ^
> 
> TypeError: cb.apply is not a function
>     at /data/soft/nodejs/lib/node_modules/gitbook-cli/node_modules/npm/node_modules/graceful-fs/polyfills.js:287:18
>     at FSReqCallback.oncomplete (fs.js:169:5)
> ```
>
> 解决办法为：https://www.cnblogs.com/cyxroot/p/13754475.html  用记事本打开，搜索fs.stat，找到那三行代码，在前面加//即可。
>
> 终于安装成功（每一步都是坑，走完这一步我花了一整个晚上，确实很想骂人）

## 初始化gitbook

首先cmd到一个目录下面，运行`gitbook init`来初始化文件，默认会生成2个文件，`README.md` 书籍的介绍写在这个文件里；`SUMMARY.md`书籍的目录结构在这里配置。

```D:\book>gitbook init
warn: no summary file in this book
info: create README.md
info: create SUMMARY.md
info: initialization is finished
```

然后在`SUMMARY.md`上面输入以下内容：

```* [前言](README.md)
* [第一章](Chapter1/README.md)
  * [第1节：衣](Chapter1/衣.md)
  * [第2节：食](Chapter1/食.md)
  * [第3节：住](Chapter1/住.md)
  * [第4节：行](Chapter1/行.md)
* [第二章](Chapter2/README.md)
* [第三章](Chapter3/README.md)
* [第四章](Chapter4/README.md)
```

再继续一次`gitbook init`，这时可以看到，gitbook就自动生成了这些目录了。再运行`gitbook serve`来预览这本书籍，执行命令后会对 Markdown 格式的文档进行转换，默认转换为 html 格式，最后提示 “Serving book on [http://localhost:4000](http://localhost:4000/) “嗯，打开浏览器看一下吧：![img](https://www.wumingx.com/assets/9df612dfc0f5bebd540837c31b9e0a7f.png)

可以看到，可以正常输出内容来了。但上图显示的是旧版的book排版，看上去会简结很多，而新版就不是这样了，这边要有疯狂吐槽中。。。

> cmd到一个目录下面，win+R之后，输入cmd，回车。然后在里面输入一个目标文件夹，可以先建好，比如我的是**D:\Github写书计划\德康减脂课** ，那么需要输入的代码为**cd /d D:\Github写书计划\德康减脂课** ，即是所谓的cmd到一个目录下面。
>
> 