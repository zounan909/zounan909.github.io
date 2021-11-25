---
title: Linux下使用KVM虚拟机安装华为OpenEuler系统
date: 2021-11-24 17:48:52
tags: [OpenEuler]
categories: 
  - Linux涨姿势
---


# 背景和优点
KVM是Kernel-based Virtual Machine的简称，是一个开源的系统虚拟化模块，从名字可以看出，是一个基于内核的虚拟化系统。

相比较于我们常用的VMware虚拟机，KVM不仅仅开源，而且基于Linux内核，其工作效率更高，这点在红帽官方得到证实。
![image](http://files.mdnice.com/user/14935/ca80263d-a82a-4e11-8e57-972542d71de6.png)
下面是红帽对KVM与VMware官方作出的说明，我把地址放在下面，有需要的朋友可以参考了解。
```
# KVM与VMware官方对比说明
https://www.redhat.com/zh/topics/virtualization/kvm-vs-vmware-comparison
```
KVM 和 VMware ESXi 都是非常成熟稳定的虚拟机监控程序，可以支持各种企业工作负载，由于KVM其开源特性，你不用再像ESXi那样为其支付许可费用，更能节约成本。
# 安装KVM
我这里依然在CentOS下搭建演示，使用Ubuntu的朋友操作类似。  
使用root用户登录到系统，使用以下命令安装KVM核心组件。
```
# 使用命令安装以下KVM核心组件
yum -y install qemu-kvm
yum -y install libvirt-daemon
yum -y install libvirt-client
yum -y install libvirt-daemon-driver-qemu
yum -y install virt-manager
```
上面各个组件的含义可参考下表：
![image](http://files.mdnice.com/user/14935/fcfac083-2a71-440a-b30d-775a422d5279.png)
安装完成后，启动libvirtd并设置为开机启动。
```shell
systemctl enable --now libvirtd
systemctl status libvirtd
```
可以看到本机上的libvirtd守护进程已经在正常运行。
![image](http://files.mdnice.com/user/14935/15723157-3ed6-41d6-b916-c36d7efcd7cb.png)
# 使用KVM图形工具
如果你的Linux有图形桌面环境，那你可能需要到桌面上去执行启动KVM图形管理工具；如果你像我一样使用的是字符下的Linux系统，根本没有安装桌面，那需要一个图形转发软件来显示图形。
比如使用NETSARANG旗下的XManager软件来转发，也就是同Xshell一家的软件。  
在Windows下安装好XManager和Xshell工具软件，使用Xshell登录到前面安装好KVM的操作系统，使用以下命令运行KVM图形管理工具。
```
virt-manager
```
执行后，会自动弹出一个窗口，如果你像我一样没有报错则成功。
![image](http://files.mdnice.com/user/14935/0753b64d-a18d-4d36-a89d-5371558e1343.png)
# 创建虚拟机
利用文件传输工具将OpenEuler传输到服务器/tmp目录下备用。
![QQ20211123-0](https://files.mdnice.com/user/14935/6cc7dd18-76a1-4fc4-9264-93c58d75b7cf.png)
回到前面的图形操作界面，在KVM里新建一个虚拟机。
![1](https://files.mdnice.com/user/14935/3688f5f5-b51b-4be5-abb7-4b7ccd875ab7.png)
选择本地的ISO镜像文件。
![2](https://files.mdnice.com/user/14935/3dd505ef-f287-4947-99a9-5d5355ccb645.png)
![3](https://files.mdnice.com/user/14935/ce41a502-2dc1-49fe-95b9-4801d39d2ea1.png)
选择本地的ISO文件，并浏览本地目录。
![4](https://files.mdnice.com/user/14935/5cdda4e9-e2d8-40e9-931a-d6a2e4ce27dc.png)
定位到文件目录/tmp下，并选定我们的安装镜像文件中。
![5](https://files.mdnice.com/user/14935/183fcb32-3edf-445e-9b8f-aebfb8a6b2bb.png)
![6](https://files.mdnice.com/user/14935/7af5c0cb-0125-4f3e-8f7f-254e8c9f7ad6.png)
![7](https://files.mdnice.com/user/14935/7242d2be-583b-48eb-ba16-0da698c1ff56.png)

配置好内存和磁盘和CPU大小。
![8](https://files.mdnice.com/user/14935/126131e1-65a9-4354-82df-199b52fd0cb7.png)
重命名下新建的虚拟机，点击完成。
![9](https://files.mdnice.com/user/14935/bbcf2c96-f0ea-4716-b098-e994c916484f.png)

最后就是我们熟悉的安装界面了。
![10](https://files.mdnice.com/user/14935/54227fb8-1cb7-42c2-9127-715b120b4ae3.png)
![11](https://files.mdnice.com/user/14935/dc97687c-c0b3-43e1-8386-8f8af979fc44.png)
