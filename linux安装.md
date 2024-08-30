首先，更新本地包列表，以确保你可以获得最新的软件包信息：

``` cmd
sudo apt-get update
```

安装vim

``` cmd
sudo apt-get install vim
```

验证

``` cmd
vim --version
```

更改默认编辑器由nano换为vim

首先确保vim安装成功

```cmd
# root执行：
sudo update-alternatives --config editor
# 选择 vim.basic后面的数字

# 验证查看默认编辑器
update-alternatives --display editor
```

![image-20240719211417184](https://image1-1324746932.cos.ap-beijing.myqcloud.com/undefinedimage-20240719211417184.png)

创建用户Alex,指定用户主目录/home/Alex，用户组为users

``` cmd
sudo useradd -m -g users Alex
```

指定密码

```cmd
sudo passwd Alex
# 输入密码
```

为Alex赋sudo权限:

```cmd
# 打开/etc/sudoers
sudo visudo
# 添加
Alex ALL=(ALL) NOPASSWD: ALL
# 或 我一般添加下面  这里需要输入的密码是Alex的密码
Alex ALL=(ALL) NOPASSWD: /usr/bin/apt-get, /bin/systemctl

# 验证
sudo apt-get update
```

![image-20240719211804406](https://image1-1324746932.cos.ap-beijing.myqcloud.com/undefinedimage-20240719211804406.png)

前面信息显示不对：

```cmd
vi ~/.bash_profile

添加一行：
export PS1='[\u@\h \W]\$ '

保存关闭，然后执行：
source ~/.bash_profile
```

![image-20240719205952391](https://image1-1324746932.cos.ap-beijing.myqcloud.com/undefinedimage-20240719205952391.png)

将sh改为bash

```cmd
chsh -s /bin/bash
# 重新登陆

# 验证默认 shell 是否已更改为 bash：
echo $SHELL
```

C++开发环境

```cmd
# 更新软件包列表
sudo apt-get update

# debian12.5默认安装# GCC 12.2 G++ 12.2：
sudo apt-get install gcc g++

# 配置gcc和g++
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-12 60
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-12 60

# 使用 update-alternatives 命令来选择默认版本。
sudo update-alternatives --config gcc
sudo update-alternatives --config g++

# 检查版本
g++ --version
gcc --version
```

![image-20240719220035705](https://image1-1324746932.cos.ap-beijing.myqcloud.com/undefinedimage-20240719220035705.png)



安装mysql

安装 Mysql 时，需要判断你的发行版，因此需要 lsb-release

```shell
sudo apt install lsb-release
```

安装 Mysql 的源。可以从这个网页获取最新版本的链接：[mysql获取](https://dev.mysql.com/downloads/repo/apt/)

![image-20240719224814471](https://image1-1324746932.cos.ap-beijing.myqcloud.com/undefinedimage-20240719224814471.png)

```shell
wget https://dev.mysql.com/get/mysql-apt-config_0.8.32-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.32-1_all.deb
# 可以不删除
rm mysql-apt-config_0.8.32-1_all.deb
```

安装


```shell
sudo apt update
sudo apt-get install mysql-server
```

修改root远程登录权限

```mysql
use mysql;
select user, host from user;
update user set host="%" where user = "root" and host="localhost";

#查询验证
select user, host from user;

# 刷新权限
flush privileges;
exit;
```

![image-20240719225336913](https://image1-1324746932.cos.ap-beijing.myqcloud.com/undefinedimage-20240719225336913.png)

### vscode远程连接linux

1. 制作密钥和公钥(windows下，确保ssh已安装)
   ``` cmd
   ssh-keygen -t rsa -b 4096
   ```

2. 这里可以选择改一下名，以便连接多个linux
   ![image-20240720001900890](https://image1-1324746932.cos.ap-beijing.myqcloud.com/undefinedimage-20240720001900890.png)

3. 将私钥上传至linux
   ``` powershell
   # 在用户文件夹下创建.ssh文件
   mkdir .ssh
   
   # 查看创建是否成功
   ls -a
   ```

4. 在windows下

   ``` cmd
   # 切换到公钥目录下
   # windows下查看当前目录 相当于ls
   dir
   # scp命令传至linux
   scp vscode_to_debian_id_rsa.pub Alex@39.105.160.22:.ssh/.
   ```

   ![image-20240720002314862](https://image1-1324746932.cos.ap-beijing.myqcloud.com/undefinedimage-20240720002314862.png)

5. 在linux下
   ``` powershell
   # 将公钥写入authorized_keys
   cat vscode_to_debian_id_rsa.pub >> authorized_keys
   ```

![image-20240720002506763](https://image1-1324746932.cos.ap-beijing.myqcloud.com/undefinedimage-20240720002506763.png)

6. 在vscode中

​	IdentityFile 设为windows下私钥位置

![image-20240720002803962](https://image1-1324746932.cos.ap-beijing.myqcloud.com/undefinedimage-20240720002803962.png)
