## webp 批量替换图片 gradle plugin


#webp转换插件使用

webp转换插件可批量转换 build时 /build/intermediates/res/${flavorName}/${buildType}目录下的图片

其搜索目标文件的规则如下

1. res下以drawable为开头的目录
2. 后缀为png,jpg的文件
3. 不包含.9图片


webp插件的运行时机是在 processXXXResource Task前 添加一个名为webpConvertPlugin的 task并执行


##webp插件使用前需要安装cwebp工具
具体方法如下：

###homebrew 安装方法：
装了brew 工具的同学可以用brew install webp

###macports 安装方法：

1. 在http://distfiles.macports.org/MacPorts/中寻找对应你系统的最新版MacPorts安装包下载并安装
2. 在终端依次运行以下命令

		export PATH=$PATH:/opt/local/bin
		sudo port selfupdate
		sudo port install webp

通过在终端键入 cwebp判断是否安装成功




安装遇到问题请参考

	https://developers.google.com/speed/webp/docs/precompiled#installing_cwebp_and_dwebp_on_os_x_with_macports
或@伯约



webp插件的使用方法如下：

1. 在外层的build.gradle文件中（即与settings.gradle同级的文件）添加如下代码

	  classpath 'com.mogujie.gradle:webpConvertPlugin:1.1.33'
2. 在内层build.gradle文件中（即与src同级的文件）添加如下代码

		apply plugin: 'webpConvert'

		webpinfo {
			//是否在debug时跳过webp转换
    		skipDebug = true
    		//是否显示log
    		isShowLog = false
		}

3.在与src同级的目录下添加名为webp_white_list.txt的文件 此文件提供白名单功能 可以设置哪些文件不会被转换为webp文件，配置时，一个文件名为一行，如

		bill_footer_sitepro_arrow.png
		cart_checkbox_false.png


好了，万事具备，只要你clean后  assemble一发，png,jpg就替换成功了，so easy
如：

gradle clean
gradle assembleDebug

如遇使用问题，请@伯约



