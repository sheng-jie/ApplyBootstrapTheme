# 引言
作为后端开发来说，前端表示玩不转，我们一般会选择套用一些开源的Bootstrap 模板主题来进行前端设计。那如何套用呢？今天就简单创建一个ASP.NET Core Web MVC 模板项目为例，来应用第三方Bootstrap Template——[Admin LTE](https://adminlte.io/)。

![AdminLte Dashboard](https://upload-images.jianshu.io/upload_images/2799767-d2ac34c68400a7f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 1. 创建ASP.NET Core MVC Demo
命令行执行`dotnet new mvc -n ApplyBootstrapTemplate`，即可创建预置的MVC模板项目。项目结构如下图：
![MVC Demo structure](https://upload-images.jianshu.io/upload_images/2799767-dd965f94822e17aa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
从项目结构来看，我们可以看到wwwroot目录下包含了css、images、js、lib目录，其中lib目录默认引用了bootstrap、jquery相关包。因为是简单的模板项目，所以UI就很将就。

# 2. 下载AdminLte
目前AdminLte在计划发布AdminLTE 3.0版本，不过现在还处于Alpha版本。我们[下载AdminLTE-V2.4.3](https://github.com/almasaeed2010/AdminLTE/releases/tag/v2.4.3)来使用。
下载后解压得到的项目结构如下：
![AdminLte Structure](https://upload-images.jianshu.io/upload_images/2799767-2ed012e496295137.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 3. 替换模板
基于AdminLTE进行开发，仅需要复制dist目录，及其依赖的bower包就可以了。
第一步：我们清空wwwroot下的全部目录（我这边暂时保留了images文件夹，后面会用到）。
第二步：然后复制dist目录到wwwroot下。

其依赖的bower包是安装在bower_components目录下的。我们无需直接复制整个bower_components文件夹，我们复制bower.json包定义文件即可。

第三步：复制AdminLTE下的bower.json到ASP.NET Core Mvc根目录下。
第四步：使用VS2017打开项目后，我们可以看到VS2017已经可以识别到未安装的Bower包。
![](https://upload-images.jianshu.io/upload_images/2799767-1f0a17b5544864f7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
右键就可以还原bower包。不过先慢着，我们现在还原就会直接还原bower包到根目录下了，并没有还原bower包到wwwroot文件夹下。
第五步：新增.bowerrc文件，配置包安装路径即可（我们指定了wwwroot\bower_components，与原始AdminLTE的目录结构保持一致的好处是，可以直接迁移AdminLTE定义的示例页面。当然我们也可以按需指定）。如图所示：
![配置bower包安装路径](https://upload-images.jianshu.io/upload_images/2799767-bc24a903fcbf869d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
第六步：Restore Package
~~第七步：将bower_components包含到项目中。（这一步可先不做）~~
![Include In Project](https://upload-images.jianshu.io/upload_images/2799767-19bd9d773c80842a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 4. 修改_Layout.cshtml
接下来我们将AdminLTE的预置起始页面starter.html移植进我们的布局页面_Layout.cshtml。
我们先来观察一下我们默认的布局页。
![](https://upload-images.jianshu.io/upload_images/2799767-7b0373ccbfcbb85a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
主要有以上几个地方需要注意。
1. 根据环境配置css和js的加载
2. @RenderBody()
3. @RenderSection("Scripts", required: false)

我们直接暴力复制starter.html的内容复制粘贴到_Layout.cshtml，然后再将以上三个点进行修改即可。然后修改引用的css、js路径即可。修改后的截图如下：
![updated _Layout.cshtml](https://upload-images.jianshu.io/upload_images/2799767-ddf65f4f031b8610.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 最终效果
CTRL+F5运行效果图如下，至此我们成功完成AdminLTE主题的应用。DEMO已上传到[Github](https://github.com/yanshengjie/ApplyBootstrapTheme)。

![](https://upload-images.jianshu.io/upload_images/2799767-c5dcba6e3cc686f1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
