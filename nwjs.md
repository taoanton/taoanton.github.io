#nwjs

##NW.js是什么？
>官方网址：http://nwjs.io/  

NW.js 是基于 `Chromium` 和 `Node.js` 运行的， 以前也叫Node-Webkit。这就给了你使用HTML和JavaScript来制作桌面应用的可能。在应用里你可以直接调用Node.js的各种api以及现有的第三方包。因为Chromium和 Node.js 的跨平台，那么你的应用也是可以跨平台的。  
 
现在已经有很多知名的应用是基于NW.js实现，这是官方统计的一些列表
> https://github.com/nwjs/nw.js/wiki/List-of-apps-and-companies-using-nw.js

下载地址：
> http://nwjs.io/


新建配置文件`package.json`  

```
{
    "name": "project name",
    "main": "src/index.html",
    "window": {
        "title": "page title",
        "toolbar": false,
        "width": 1920,
        "height": 1080,
        "resizable": true
    }
}
```
**name**:项目名称   
**main**:启动文件  
**window**:窗口设置  
> 更多配置参数: https://github.com/nwjs/nw.js/wiki/Manifest-format

新建src/index.html文件，压缩`package.json`和`src`目录,压缩包名`nwtest.zip`,压缩里的目录结构

```
package.json
src/
	index.html
```
修改压缩包名，改为`nwtest.nw`

执行命令  

```
//mac可通过nwjs执行文件运行
./nwjs nwtest.nw
```
**打包可执行文件**  
mac osx可以修改`nwtest.nw`打开方式，使用`nwjs.app`打开，
或者拷贝应用程序里的`nwjs.app`，重命名为`nwtest.app`,右键`显示报内容`，拷贝nwtest.nw到`Contents/Resources`目录，
此时就可以当做一个双击运行应用了。

windows 通过命令打包

```
copy /b nw.exe+nwtest.nw start.exe
```
windows可以通过[Enigma Virtual Box](http://enigmaprotector.com/en/aboutvb.html)打包成一个独立的运行文件。
> 打包文档：https://github.com/nwjs/nw.js/wiki/How-to-package-and-distribute-your-apps




参考文档：
> https://github.com/nwjs/nw.js/wiki/Window
> https://github.com/nwjs/nw.js/wiki/How-to-run-apps
> https://github.com/nwjs/nw.js/wiki/List-of-apps-and-companies-using-nw.js
> https://github.com/nwjs/nw.js/wiki/How-to-package-and-distribute-your-apps
> https://github.com/nwjs/nw.js/wiki/Icons
> https://github.com/nwjs/nw-builder#optionswinico