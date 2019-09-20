# 项目介绍

在mac、raspberrypi下，实现与服务器进行便捷的文件上传和下载操作


# 步骤

## Mac

1.安装支持rz和sz命令的lrzsz：
`brew install lrzsz`


2.在本地/usr/local/bin/目录下保存iterm2-send-zmodem.sh 和iterm2-recv-zmodem.sh两个脚本。可以直接copy，也可以直接vim命令行创建。

查看创建创建的文件权限

```
appledeMacBook-Pro:bin user$ ls -l /usr/local/bin/iterm2-*
-rw-r--r--  1 user  admin  1010  9 20 17:10 /usr/local/bin/iterm2-recv-zmodem.sh
-rw-r--r--  1 user  admin   932  9 20 17:10 /usr/local/bin/iterm2-send-zmodem.sh
```

3.设置一下两个脚本的权限，一般 chmod 777 就行了

```bash
chmod 777 /usr/local/bin/iterm2-*
```

4.设置Iterm2的Tirgger特性，profiles->default->editProfiles->Advanced中的Tirgger

添加两条trigger，分别设置 Regular expression，Action，Parameters，Instant如下：

```
1.第一条
        Regular expression: rz waiting to receive.\*\*B0100
        Action: Run Silent Coprocess
        Parameters: /usr/local/bin/iterm2-send-zmodem.sh
        Instant: checked
2.第二条
        Regular expression: \*\*B00000000000000
        Action: Run Silent Coprocess
        Parameters: /usr/local/bin/iterm2-recv-zmodem.sh
        Instant: checked
```

![如图](https://github.com/aikuyun/iterm2-zmodem/blob/master/imgs/01.png)


## Raspberrypi

pi@raspberrypi:/usr/local/bin/lrzsz-0.12.20
```
su root 
wget -c http://www.ohse.de/uwe/releases/lrzsz-0.12.20.tar.gz
tar -zxvf lrzsz-0.12.20.tar.gz
cd lrzsz-0.12.20/
./configure
make 
make install
```
查看安装情况
```
root@raspberrypi:/usr/local/bin# ls -l
total 1744
-rwxr-xr-x 1 root staff    219 Jun 12 13:53 docker-compose
-rwxr-xr-x 1 root staff    233 Dec 22  2018 easy_install
-rwxr-xr-x 1 root staff    233 Dec 22  2018 easy_install-2.7
-rwxr-xr-x 1 root staff    217 Jun 12 11:50 jsonschema
-rwxr-xr-x 3 root staff 222924 Sep 20 18:02 lrb
-rwxr-xr-x 3 root staff 222924 Sep 20 18:02 lrx
-rwxr-xr-x 3 root staff 222924 Sep 20 18:02 lrz
drwxrwxrwx 9  406 disk    4096 Sep 20 18:00 lrzsz-0.12.20
-rw-r--r-- 1 root staff 280938 Dec 31  1998 lrzsz-0.12.20.tar.gz
-rwxr-xr-x 3 root staff 231372 Sep 20 18:02 lsb
-rwxr-xr-x 3 root staff 231372 Sep 20 18:02 lsx
-rwxr-xr-x 3 root staff 231372 Sep 20 18:02 lsz
-rwxr-xr-x 1 root staff  35097 Sep 11 10:02 miniterm.py
-rw-r--r-- 1 root staff  36151 Sep 11 10:02 miniterm.pyc
-rwxr-xr-x 1 root staff    214 Sep 11 09:59 pip
-rwxr-xr-x 1 root staff    214 Sep 11 09:59 pip2
-rwxr-xr-x 1 root staff    214 Sep 11 09:59 pip2.7
drwxr-sr-x 2 root staff   4096 Jun 12 11:50 __pycache__
-rwxr-xr-x 1 root staff    219 Sep 11 10:02 pymodbus.console
-rwxr-xr-x 1 root staff    211 Dec 22  2018 wheel
-rwxr-xr-x 1 root staff   5902 Jun 12 11:50 wsdump.py
```

配置软链接
```
root@raspberrypi:/usr/local/bin# ln -s lrz rz
root@raspberrypi:/usr/local/bin# ln -s lsz sz

root@raspberrypi:/usr/local/bin# ls -l
total 1744
-rwxr-xr-x 1 root staff    219 Jun 12 13:53 docker-compose
-rwxr-xr-x 1 root staff    233 Dec 22  2018 easy_install
-rwxr-xr-x 1 root staff    233 Dec 22  2018 easy_install-2.7
-rwxr-xr-x 1 root staff    217 Jun 12 11:50 jsonschema
-rwxr-xr-x 3 root staff 222924 Sep 20 18:02 lrb
-rwxr-xr-x 3 root staff 222924 Sep 20 18:02 lrx
-rwxr-xr-x 3 root staff 222924 Sep 20 18:02 lrz
drwxrwxrwx 9  406 disk    4096 Sep 20 18:00 lrzsz-0.12.20
-rw-r--r-- 1 root staff 280938 Dec 31  1998 lrzsz-0.12.20.tar.gz
-rwxr-xr-x 3 root staff 231372 Sep 20 18:02 lsb
-rwxr-xr-x 3 root staff 231372 Sep 20 18:02 lsx
-rwxr-xr-x 3 root staff 231372 Sep 20 18:02 lsz
-rwxr-xr-x 1 root staff  35097 Sep 11 10:02 miniterm.py
-rw-r--r-- 1 root staff  36151 Sep 11 10:02 miniterm.pyc
-rwxr-xr-x 1 root staff    214 Sep 11 09:59 pip
-rwxr-xr-x 1 root staff    214 Sep 11 09:59 pip2
-rwxr-xr-x 1 root staff    214 Sep 11 09:59 pip2.7
drwxr-sr-x 2 root staff   4096 Jun 12 11:50 __pycache__
-rwxr-xr-x 1 root staff    219 Sep 11 10:02 pymodbus.console
lrwxrwxrwx 1 root staff      3 Sep 20 18:04 rz -> lrz
lrwxrwxrwx 1 root staff      3 Sep 20 18:05 sz -> lsz
-rwxr-xr-x 1 root staff    211 Dec 22  2018 wheel
-rwxr-xr-x 1 root staff   5902 Jun 12 11:50 wsdump.py
root@raspberrypi:/usr/local/bin#
```


