# Github + Hexo 搭建个人博客


本文内容主要讲解如何利用 Hexo + Github Page 搭建个人博客，内容包含基本工具（Node.js、Git、Github、Hexo）的安装使用、如何利用Hexo进行发布、修改、删除文章、图片添加水印等细节。

<!--more-->

> 本文修改自【韦阳】的博客《超详细Hexo+Github博客搭建小白教程》 
>
> 原文链接：https://godweiyang.com/2018/04/13/hexo-blog/
>
> 遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。

## 快速搭建

已经搭建和配置好的模板：https://github.com/zz2summer/blog-hexo-theme-matery.git，下载后，先解压 `node_modules.zip`，然后删除 `.git`

如果出现bug，可能是npm版本等问题，可以把 node_moudules 文件删除，重新安装对应模块组件

## 安装Node.js

官网下载：[Node.js](https://nodejs.org/en/)

安装直接点击 `Next` 即可

最后测试是否安装成功：

用 `win + R` 打开命令行提示符，输入 `cmd`，之后输入命令：`node -v`、`npm -v`，如果显示版本号即安装成功！

![image-20210324155112598](/Github+Hexo搭建个人博客/image-20210324155112598.png)

## 添加国内镜像源

可以切换使用阿里的国内镜像对 npm 进行加速

```bash
# 设置自定义镜像命令
npm config set registry https://registry.npm.taobao.org

# 查看npm源地址
npm config list

# 删除自己设置的镜像命令
npm config rm registry
```

## 安装 Git

下载分布式版本管理工具 [Git](https://git-scm.com/download/win) —— 主要用于之后把本地网页部署到 Github 上去

安装选项还是全部默认，只不过最后一步添加路径时选择`Use Git from the Windows Command Prompt`，这样我们就可以直接在命令提示符里打开git了。

安装完成后在命令提示符中输入`git --version`验证是否安装成功。

## 注册 Github

打开https://github.com/，新建一个项目，如下所示：

![image-20210324160452279](/Github+Hexo搭建个人博客/image-20210324160452279.png)

然后如下图所示，输入自己的项目名字，后面一定要加`.github.io`后缀，README初始化也要勾上。**名称一定要和你的github名字完全一样，比如你github名字叫`abc`，那么仓库名字一定要是`abc.github.io`。**

![image-20210324160630054](/Github+Hexo搭建个人博客/image-20210324160630054.png)

然后项目就建成了，点击`Settings`，向下拉到最后有个`GitHub Pages`，点击`Choose a theme`选择一个主题。然后等一会儿，再回到`GitHub Pages`，会变成下面这样：

![image-20210324160907940](/Github+Hexo搭建个人博客/image-20210324160907940.png)

点击那个链接，就会出现自己的网页啦，效果如下：

![image-20210324160943324](/Github+Hexo搭建个人博客/image-20210324160943324.png)

## 安装Hexo

在合适的地方新建一个文件夹，用来存放自己的博客文件，比如我的博客文件都存放在`H:\blog`目录下。

在该目录下右键点击`Git Bash Here`，打开git的控制台窗口，以后我们所有的操作都在git控制台进行，就不要用Windows自带的控制台了。

定位到该目录下，输入`npm i hexo-cli -g`安装Hexo。会有几个报错，无视它就行。

![image-20210324161557954](/Github+Hexo搭建个人博客/image-20210324161557954.png)

安装完后输入`hexo -v`验证是否安装成功。

![image-20210324161614078](/Github+Hexo搭建个人博客/image-20210324161614078.png)

然后就要初始化我们的网站，输入`hexo init`初始化文件夹，接着输入`npm install`安装必备的组件。

![image-20210324161716656](/Github+Hexo搭建个人博客/image-20210324161716656.png)

![image-20210324161846702](/Github+Hexo搭建个人博客/image-20210324161846702.png)

这样本地的网站配置也弄好啦，输入`hexo g`生成静态网页，然后输入`hexo s`打开本地服务器，然后浏览器打开http://localhost:4000/，就可以看到我们的博客啦，效果如下：

![image-20210324162007491](/Github+Hexo搭建个人博客/image-20210324162007491.png)

按`ctrl+c`关闭本地服务器。

## 连接Github与本地

首先右键打开git bash，然后输入下面命令：

```bash
git config --global user.name "zz2summer"
git config --global user.email "xxxxx@163.com"
```

用户名和邮箱根据你注册github的信息自行修改。

然后生成密钥SSH key：

```bash
ssh-keygen -t rsa -C "summer2zz@163.com"
```

按照提示直接一路回车即可。

打开 [github](http://github.com/)，在头像下面点击`settings`，再点击`SSH and GPG keys`，新建一个SSH，名字随便。

git bash中输入

```bash
cat ~/.ssh/id_rsa.pub
```

将输出的内容复制到新建 SSH的框中，点击确定保存。

输入`ssh -T git@github.com`，如果如下图所示，出现你的用户名，那就成功了。

![image-20210324163106729](/Github+Hexo搭建个人博客/image-20210324163106729.png)

打开博客根目录下的`_config.yml`文件，这是博客的配置文件，在这里你可以修改与博客相关的各种信息。

修改最后一行的配置：

```bash
deploy:
  type: git
  repository: https://github.com/zz2summer/zz2summer.github.io
  branch: master
```

repository修改为你自己的github项目地址。

## 写文章、发布文章

首先在博客根目录下右键打开git bash，安装一个扩展`npm i hexo-deployer-git`。

![image-20210324163528734](/Github+Hexo搭建个人博客/image-20210324163528734.png)

然后输入`hexo new post "article title"`，新建一篇文章。

![image-20210324163542106](/Github+Hexo搭建个人博客/image-20210324163542106.png)

然后打开`H:\blog\source\_posts`的目录，可以发现下面多了一个`article-title.md`文件，就是文章文件。

编写完markdown文件后，根目录下输入`hexo g`生成静态网页，然后输入`hexo s`可以本地预览效果，最后输入`hexo d`上传到github上。这时打开你的github.io主页就能看到发布的文章啦。

![image-20210324165901906](/Github+Hexo搭建个人博客/image-20210324165901906.png)



如果需要上传图片，需要修改配置文件`_config.yml`来生成。

`post_asset_folder: true`

这样每次新建文件就会直接生成文章和同名文件夹，图片放到文件夹中再用相对路径引用图片即可。

## 图片添加水印

为了防止别人抄袭你文章，可以把所有的图片都加上水印，方法很简单。

首先在博客根目录下新建一个`watermark.py`，代码如下：

```python
# -*- coding: utf-8 -*-
import sys
import glob
from PIL import Image
from PIL import ImageDraw
from PIL import ImageFont


def watermark(post_name):
    if post_name == 'all':
        post_name = '*'
    dir_name = 'source/_posts/' + post_name + '/*'
    for files in glob.glob(dir_name):
        im = Image.open(files)
        if len(im.getbands()) < 3:
            im = im.convert('RGB')
            print(files)
        font = ImageFont.truetype('STSONG.TTF', max(30, int(im.size[1] / 20)))
        draw = ImageDraw.Draw(im)
        text_size_x, text_size_y = draw.textsize(u'@yourname', font=font)
        draw.text((im.size[0] - text_size_x, im.size[1] - text_size_y), u'@yourname', fill=(0, 0, 0, 85), font=font)
        im.save(files)


if __name__ == '__main__':
    if len(sys.argv) == 2:
        watermark(sys.argv[1])
    else:
        print('[usage] <input>')
```

字体也放根目录下，自己找字体。（win10自带字体文件目录：C:\Windows\Fonts）然后每次写完一篇文章可以运行`python watermark.py postname`添加水印，如果第一次运行要给所有文章添加水印，可以运行`python watermark.py all`。

如果报错显示：`ModuleNotFoundError: No module named 'PIL'`，意思没有安装对应的 Python 模块，运行命令：`pip install Pillow`



## 修改样式

建议参考官方说明文档：[hexo-theme-matery/README_CN.md at develop · blinkfox/hexo-theme-matery](https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md)

详细而且是最新的。

注意区分博客的配置文件和主题的配置文件，基本上把两个配置文件浏览一遍，基本配置就改好了。

## 文章基本操作

### 发表文章

```bash
# 新建文章
hexo new post "article title"

# 图片加水印
# 单篇文章 postname
python watermark.py postname
# 所有文章
python watermark.py all

# 生成静态页面
hexo g

# 本地预览
hexo s

# 部署到网站
hexo d
```

### 修改文章

修改对应文章内容，然后执行命令 `hexo d -g` 即可。

### 删除文章

删除目录 `source\_posts` 下对应文章文件，然后执行命令 `hexo d -g` 即可。

### 其他

1. 多个标签：[标签1,标签2,标签3]
2. 插入上传图片
   - 将图片放置在在 .md 同级目录下的同名文件夹下，引用时**直接写图片名**即可，如：`![](pic_name.png)`，部署后该HTML页面和图片位于同级目录
   - 将图片放置在在 `source/images` 目录下，引用时使用`![](/images/pic_name.png)`



## Hexo 常见操作

```bash
# Create a new post
$ hexo new "My New Post"

# Run server
$ hexo server

# Generate static files
$ hexo generate

# Deploy to remote sites
$ hexo deploy

# 清空缓存并生成新的静态页面
hexo clean && hexo g
```



## 遇到的问题

因为开了代理，所以连接上可能会出现一些问题

```bash
Summer@DESKTOP-NU751AT MINGW64 /h/blog/themes
$ git clone https://github.com/blinkfox/hexo-theme-matery.git
Cloning into 'hexo-theme-matery'...
fatal: unable to access 'https://github.com/blinkfox/hexo-theme-matery.git/': OpenSSL SSL_read: Connection was reset, errno 10054

Summer@DESKTOP-NU751AT MINGW64 /h/blog/themes
$ git config --global http.proxy 127.0.0.1:8580
```



## 参考文章

【1】[超详细Hexo+Github博客搭建小白教程 | 韦阳的博客](https://godweiyang.com/2018/04/13/hexo-blog/)

【2】[Hexo博客主题之hexo-theme-matery的介绍 | 闪烁之狐](http://blinkfox.com/2018/09/28/qian-duan/hexo-bo-ke-zhu-ti-zhi-hexo-theme-matery-de-jie-shao/#!)

【3】[hexo-theme-matery/README_CN.md at develop · blinkfox/hexo-theme-matery](https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md)
