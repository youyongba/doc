# 如何为根分区扩容（centos7为例）
> linux系统所有的文件都是存放在根分区中的，如果根分区容量即将耗尽，我们就需要给根分区扩容，我们可以使用lsblk命令来查看，系统的根分区实际是逻辑卷，所以想要扩展根分区只要将逻辑卷扩容就可以了。此时我的根分区容量为17G，已用12G，我想要给它扩展容量应该怎么做呢

## 参考的原文

> 怕网站没有了找不到

- https://www.cnblogs.com/Agnostida-Trilobita/p/11434943.html

## 查看磁盘
```shell
[root@v1 ~]# df -h
文件系统             容量  已用  可用 已用% 挂载点
/dev/mapper/cl-root   17G   12G  5.8G   66% /
devtmpfs             478M     0  478M    0% /dev
tmpfs                489M     0  489M    0% /dev/shm
tmpfs                489M  6.7M  482M    2% /run
tmpfs                489M     0  489M    0% /sys/fs/cgroup
/dev/sda1           1014M  139M  876M   14% /boot
tmpfs                 98M     0   98M    0% /run/user/0
/dev/sr0             4.1G  4.1G     0  100% /mnt

[root@v1 ~]# lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda           8:0    0   20G  0 disk 
├─sda1        8:1    0    1G  0 part /boot
└─sda2        8:2    0   19G  0 part 
  ├─cl-root 253:0    0   17G  0 lvm  /
  └─cl-swap 253:1    0    2G  0 lvm  [SWAP]
sr0          11:0    1  4.1G  0 rom  /mnt
```

## 新添加一块硬盘
> 已经创建好了一个分区


```shell
[root@v1 ~]# lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda           8:0    0   20G  0 disk 
├─sda1        8:1    0    1G  0 part /boot
└─sda2        8:2    0   19G  0 part 
  ├─cl-root 253:0    0   17G  0 lvm  /
  └─cl-swap 253:1    0    2G  0 lvm  [SWAP]
sdb           8:16   0   10G  0 disk 
sr0          11:0    1  4.1G  0 rom
```

## 将新添加的磁盘创建分区

```shell


[root@v1 ~]# fdisk /dev/sdb
欢迎使用 fdisk (util-linux 2.23.2)。

更改将停留在内存中，直到您决定将更改写入磁盘。
使用写入命令前请三思。

Device does not contain a recognized partition table
使用磁盘标识符 0x0d87e961 创建新的 DOS 磁盘标签。

命令(输入 m 获取帮助)：n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): 
Using default response p
分区号 (1-4，默认 1)：
起始 扇区 (2048-20971519，默认为 2048)：
将使用默认值 2048
Last 扇区, +扇区 or +size{K,M,G} (2048-20971519，默认为 20971519)：
将使用默认值 20971519
分区 1 已设置为 Linux 类型，大小设为 10 GiB
命令(输入 m 获取帮助)：w
The partition table has been altered!

Calling ioctl() to re-read partition table.
正在同步磁盘。

[root@v1 ~]# lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda           8:0    0   20G  0 disk 
├─sda1        8:1    0    1G  0 part /boot
└─sda2        8:2    0   19G  0 part 
  ├─cl-root 253:0    0   17G  0 lvm  /
  └─cl-swap 253:1    0    2G  0 lvm  [SWAP]
sdb           8:16   0   10G  0 disk 
└─sdb1        8:17   0   10G  0 part 
sr0          11:0    1  4.1G  0 rom

```


## 将创建好的物理卷扩展到根分区所在卷组

```shell

[root@v1 ~]# vgdisplay -v
  --- Volume group ---
  VG Name               cl
  System ID             
  Format                lvm2
  Metadata Areas        2
  Metadata Sequence No  4
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               2
  Max PV                0
  Cur PV                2
  Act PV                2
  VG Size               28.99 GiB
  PE Size               4.00 MiB
  Total PE              7422
  Alloc PE / Size       4863 / 19.00 GiB
  Free  PE / Size       2559 / 10.00 GiB
  VG UUID               oKc6Ae-l0QZ-xNir-7U0d-sH4K-HTtN-RDm4hl
   
  --- Logical volume ---
  LV Path                /dev/cl/swap
  LV Name                swap
  VG Name                cl
  LV UUID                6ENYna-OkIl-avmF-m977-tE4z-8iCO-VyVC44
  LV Write Access        read/write
  LV Creation host, time localhost.localdomain, 2019-05-29 19:59:53 +0800
  LV Status              available
  # open                 2
  LV Size                2.00 GiB
  Current LE             512
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:1
   
  --- Logical volume ---
  LV Path                /dev/cl/root　　这个是根分区所挂载的逻辑卷路径
  LV Name                root
  VG Name                cl　　这个是根分区所在卷组名字
  LV UUID                IS5BXN-jIrh-lrr5-mp7O-SAU5-YLSt-MMWcdC
  LV Write Access        read/write
  LV Creation host, time localhost.localdomain, 2019-05-29 19:59:53 +0800
  LV Status              available
  # open                 1
  LV Size                17.00 GiB
  Current LE             4351
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:0
   
  --- Physical volumes ---
  PV Name               /dev/sda2     
  PV UUID               YRWhHU-7nfd-cJkw-uhNG-iW7U-Z8ZB-3n2IHG
  PV Status             allocatable
  Total PE / Free PE    4863 / 0

  PV Name               /dev/sdb1     
  PV UUID               OIu5Ny-VPsy-w0f8-O1Y1-QtOU-Ayey-3Hb9Om
  PV Status             allocatable
  Total PE / Free PE    2559 / 2559　　我们发现此物理卷上可用的PE为全部

  ```

## 扩展卷组容量

```shell
[root@v1 ~]# vgextend cl /dev/sdb1
  Volume group "cl" successfully extended
```


## 扩展根分区所挂载的逻辑卷路径并使扩容生效

```shell

[root@v1 ~]# lvextend -l +100%FREE /dev/cl/root　　将剩余可用容量全部扩展到/dev/cl/root
  Size of logical volume cl/root changed from 17.00 GiB (4351 extents) to 26.99 GiB (6910 extents).
  Logical volume cl/root successfully resized.

[root@v1 ~]# xfs_growfs /dev/cl/root
meta-data=/dev/mapper/cl-root    isize=512    agcount=4, agsize=1113856 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0 spinodes=0
data     =                       bsize=4096   blocks=4455424, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal               bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
data blocks changed from 4455424 to 707584
```

## 查看扩展后的根分区容量

```shell


[root@v1 ~]# lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda           8:0    0   20G  0 disk 
├─sda1        8:1    0    1G  0 part /boot
└─sda2        8:2    0   19G  0 part 
  ├─cl-root 253:0    0   27G  0 lvm  /
  └─cl-swap 253:1    0    2G  0 lvm  [SWAP]
sdb           8:16   0   10G  0 disk 
└─sdb1        8:17   0   10G  0 part 
  └─cl-root 253:0    0   27G  0 lvm  /
sr0          11:0    1  4.1G  0 rom  

[root@v1 ~]# df -h
文件系统             容量  已用  可用 已用% 挂载点
/dev/mapper/cl-root   27G   12G   16G   42% /　　根分区容量已经被扩展到27G
devtmpfs             478M     0  478M    0% /dev
tmpfs                489M     0  489M    0% /dev/shm
tmpfs                489M  6.7M  482M    2% /run
tmpfs                489M     0  489M    0% /sys/fs/cgroup
/dev/sda1           1014M  139M  876M   14% /boot
tmpfs                 98M     0   98M    0% /run/user/0

```




