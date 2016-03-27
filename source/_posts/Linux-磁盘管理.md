---
title: Linux--磁盘管理
date: 2016-03-19 14:46:59
tags: Linux
---

　　硬盘，IO设备，设备名称`IDE硬盘为hdx（x为从a—d硬盘最多四个）`，SCSI，SATA，USB硬盘为sdx（x为a—z））。`硬盘主分区最多为4个（sdb1-sdb4），逻辑分区从sdb5开始`。

<!-- more -->

### 查看磁盘信息

#### df命令

查看已挂载磁盘的总容量、使用容量、剩余容量

``` bash
df -i #使用inodes 显示结果
df -h #用合适的单位显示,G,M等
df -k #显示单位K
df –m #显示单位M
```

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160314155228.png)

说明：

> Filesystem #表示扇区,划分磁盘时所分的区
> Used #已使用
> Available #剩余
> Use% #已经使用的百分比
> Mounted on #扇区挂载点


#### du命令
 
查看某个文件

``` bash
du [-abckmsh] [文件或者目录名]
du -a #全部文件与目录大小都列出来,如果不加参数列出目录（包含子目录）。
du -h #用合适的单位显示, 还有单位-b -k –m。
du -s #只显示总和。
du -c #最后显示总和。
```

![](http://7xrw5k.com1.z0.glb.clouddn.com/blog%2Fimg%2F20160314155228.png)

### 磁盘挂载

硬盘分区及挂载操作步骤：
> 1. **`fdisk -l `**#查看未挂载的硬盘（名称为/dev/xvdb）
> Disk /dev/xvdb doesn't contain a valid partition table
> 2. **`fdisk /dev/xvdb`**  # 创建分区
> 3. 输入n
> Command (m for help):n
> 4. 输入p
> Command action
> e extended
> p primary partition (1-4)
> p
> 5. 输入1
> Partition number (1-4): 1
> 6. 回车
> First cylinder (1-2610, default 1): 
> Using default value 1
> 7. 回车
> Last cylinder, +cylinders or +size{K,M,G} (1-2610, default 2610): 
> Using default value 2610
> 8. 输入w
> Command (m for help): w
> The partition table has been altered!
> 9. **`mkfs.ext3 /dev/xvdb1`** #格式化分区
> 10. **`mkdir /data`** #建立挂载目录
> 11. **`mount /dev/xvdb1`** /data  #挂载分区
> 12. **`vi /etc/fstab`**  #设置开机自动挂载
> 在vi中输入i进入INERT模式，将光标移至文件结尾处并回车，将下面的内容复制/粘贴，然后按Esc键，输入:x保存并退出
> /dev/xvdb               /data                   ext3    defaults        0 0
> 13. **`reboot`** #重启服务器
> 14. **`df`** #查看硬盘分区
> /dev/xvdb             20635700    176196  19411268   1% /data
