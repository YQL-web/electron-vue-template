# electron + vue 实践项目

#### 本地安装环境准备
* 安装node： * https://nodejs.org/en/download/
* 配置webpack： npm install -g webpack(sudo权限)

#### 依赖包安装
* 执行cnpm install

#### 安装问题
1.执行npm install，npm 在国内比较慢，所以采用淘宝镜像代理，执行以下命令：
2.安装cnpm:$ npm install -g cnpm --registry=https://registry.npm.taobao.org,执行命令：cnpm install(z执行命令前，删除moudles文件)
3.安装完成后执行启动命令npm run dev
4.项目打包命令 npm run build,发现会报错：
意思是说打包所需的依赖文件electron-v1.7.9-win32-x64.zip下载失败，此时，可以去淘宝镜像文件库找到对应的文件并下载，放到指定的目录下，electron的淘宝镜像地址：https://npm.taobao.org/mirrors/electron/
5.下载完成后，文件应该放到哪里，一般为C:\Users\Administrator\AppData\Local\electron\Cache，你也可以全局搜索 electron-v1.7.9-win32-x64.zip，看下对应的文件下载到哪里，哪里就是你应该拷文件的位置。
6.继续执行npm run build,如果你的electron-v1.7.9-win32-x64.zip文件位置放置正确，就会继续下载SHASUMS256.txt-1.7.9，这个文件较小，容易成功。不成功的也从镜像里拷贝，注意文件结尾的版本号，此文件的位置与electron-v1.7.9-win32-x64.zip在同一个文件夹。
7. electron-v1.7.9-win32-x64.zip与SHASUMS256.txt-1.7.9两个文件是electron打包必须的文件，用于打exe文件，electron-builder打包也需要两个文件：
1）.打包成文件夹及绿色免安装：
    electron-builder --dir（依赖winCodeSign）
2）.打包成exe的安装包
    electron-builder （依赖winCodeSign和nsis）
如果这两个文件也没有下载下来，按照如下步骤操作：
8.在%LOCALAPPDATA%（C:\Users\Administrator\AppData\Local）目录下新建electron-builder\cache\，正常情况下目录是存在的。
9.下载wincodesign包，链接：https://github.com/electron-userland/electron-builder-binaries/releases,选择Source code (zip)下载并解压
10.将Source code (zip)解压后的文件拷贝到C:\Users\Administrator\AppData\Local\ electron-builder\cache\下
11.此时还需要下载winCodeSign和nsis文件，链接地址分别为：
https://github.com/electron-userland/electron-builder-binaries/releases/tag/winCodeSign-1.9.0 ，
https://github.com/electron-userland/electron-builder-binaries/releases/tag/nsis-resources-3.0.0
这两个链接我们都下载Source code (zip)文件，速度比较快，解压
12.先来配置winCodeSign，在文件夹C:\Users\Administrator\AppData\Local\electron-builder\cache\winCodeSign，新建文件winCodeSign-1.9.0，新建的文件夹名字需要和npm run build是要求下载的文件名一致，后面的nsis，以及nsis-resources同理
而后把下载的问价夹electron-builder-binaries-winCodeSign-1.9.0\winCodeSign内的文件拷贝到C:\Users\Administrator\AppData\Local\electron-builder\cache\winCodeSign\winCodeSign-1.9.0内。
13.nsis与nsis-resources的配置同理，分别创建了nsis-3.0.1.13和nsis-resources-3.3.0文件夹，把下载的文件electron-builder-binaries-nsis-resources-3.0.0\nsis\和\electron-builder-binaries-nsis-resources-3.0.0\nsis-resources\文件夹里的内容拷贝到对应的路径里。
至此配置完成，打包不会报错。

dev:

$ npm run dev
# express开启服务，可以通过`http://localhost:port`访问（热重载）
# 运行`electron ./`,生成桌面应用
# 原理：通过electron创建主体窗口，`mainWindow.loadURL(http://localhost:port)`，加载应用的 index.html

prod:

$ npm run build
#参考package.json里的打包命令,为不同环境进行打包（目前只支持window）
对于打包工具，这里使用的是`electron-packager`


