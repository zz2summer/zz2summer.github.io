# Linux下杀毒软件clamav0.104.2离线安装及测试（CentOS7）


本文主要是讲解如何在 Linux 环境下离线安装以及测试杀毒软件 clamav 0.104.2（以CentOS7为例），包括下载安装、配置参数和运行。

<!--more-->

> 版权声明：本文为博主原创文章，遵循 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 版权协议，禁止商用，转载请附上原文出处链接和本声明。

## 1.下载安装

[clamav](https://www.clamav.net/downloads) 官网下载 [clamav-0.104.2.linux.x86_64.rpm](https://www.clamav.net/downloads/production/clamav-0.104.2.linux.x86_64.rpm)

![image-20220220202514187](/Linux下杀毒软件clamav离线安装及测试（CentOS7）/image-20220220202514187.png)

将该文件上传至服务器，安装命令如下：

```bash
rpm -ivh --prefix=/usr/local/clamav clamav-0.104.2.linux.x86_64.rpm
```

## 2. 配置

1. 添加用户组和组成员

   ```bash
   groupadd clamav
   useradd -g clamav clamav
   ```

2. 创建日志目录和病毒库目录

   ```bash
   mkdir -p /usr/local/clamav/logs
   mkdir -p /usr/local/clamav/update
   ```

3. 创建日志文件

   ```bash
   touch /usr/local/clamav/logs/clamd.log
   touch /usr/local/clamav/logs/freshclam.log
   ```

3. 文件授权

   ```bash
   chown clamav:clamav /usr/local/clamav/logs/clamd.log
   chown clamav:clamav /usr/local/clamav/logs/freshclam.log
   chown clamav:clamav /usr/local/clamav/update
   ```

4. 修改配置文件

   ```bash
   cp  /usr/local/clamav/etc/clamd.conf.sample /usr/local/clamav/etc/clamd.conf
   cp /usr/local/clamav/etc/freshclam.conf.sample /usr/local/clamav/etc/freshclam.conf
   ```
   
   文件1：clamd.conf
   
   ```bash
   vim /usr/local/clamav/etc/clamd.conf
   ```
   
   ```bash
   #Example　　//注释掉这一行
   #添加以下内容
   LogFile /usr/local/clamav/logs/clamd.log
   PidFile /usr/local/clamav/update/clamd.pid
   DatabaseDirectory /usr/local/clamav/update
   ```
   
   文件2：freshclam.conf
   
   ```bash
   vim /usr/local/clamav/etc/freshclam.conf
   ```
   
   ```bash
   #Example　　//注释掉这一行
   #添加以下内容
   DatabaseDirectory /usr/local/clamav/update
   UpdateLogFile /usr/local/clamav/logs/freshclam.log
   PidFile /usr/local/clamav/update/freshclam.pid
   ```
   
   将这两个文件复制一下：
   
   ```bash
   cp /usr/local/clamav/etc/*.conf /usr/local/etc/
   ```

## 3. 运行

1. 下载病毒库文件并上传到目录 **/usr/local/clamav/update**

   [main.cvd](http://database.clamav.net/main.cvd)
   [daily.cvd](http://database.clamav.net/daily.cvd)
   [bytecode.cvd](http://database.clamav.net/bytecode.cvd)

   注：也可以在有网络的机器上运行如下命令更新病毒库：

   ```bash
   /usr/local/clamav/bin/freshclam
   ```

2. 配置库文件路径

   ```bash
   vim /etc/ld.so.conf
   ```

   追加一行：

   ```bash
   /usr/local/clamav/lib64
   ```

   更新生效：

   ```bash
   ldconfig
   ```

   如果最后运行时仍然报错：

   ```bash
   clamscan: error while loading shared libraries: libclamav.so.9: cannot open shared object file: No such file or directory
   ```

   则说明配置没有生效。

3. 创建命令软件链接

   ```bash
   ln -s /usr/local/clamav/bin/clamscan /usr/local/bin/clamscan
   ```

4. 运行使用

   ```bash
   clamscan -r
   ```

   ![image-20220220210854780](/Linux下杀毒软件clamav离线安装及测试（CentOS7）/image-20220220210854780.png)
   
5. 卸载程序

   ```bash
   rpm remove clamav
   ```

   

