20240309 安装pve及桌面xfce4、scim，在pve下安装苹果
记录


1、参考资料3份：
    a. https://blog.csdn.net/weixin_44293949/article/details/121863559 解决raw.githubusercontent.com无法访问的问题 
    b. https://github.com/luchina-gabriel/OSX-PROXMOX Run macOS on ANY Computer - AMD & Intel
    c. https://github.com/kholia/OSX-KVM  Run macOS on QEMU/KVM. With OpenCore + Monterey + Ventura + Sonoma support now!

2、nano /etc/hosts
    ![image](https://github.com/nophook/pve-xfce4-scim-macOS-passthrogh/assets/113235819/3b2f3403-d02e-4681-a458-850880e76b32)

3、方案建议
    b／c任一方案都可以，交叉组合也可以（我用b的recovery-ventura.iso,800M,配合c的OpenCore-v20.iso,157M），最终建议用b，脚本自动建好虚拟机和磁盘

4、pve安装桌面及汉化
    apt install xfce4 scim-pinyin
    根据依赖会自动安装其他组件。
    Applications -- Settings -- Appearence -- Fonts -- Default Font 选正体中文字体，我是选的WenQuanYi Micro Hei Regular，效果类似新宋。
    scim套件安装仅130M，比较节约。

    切换图形桌面配套：
    nano /etc/default/grub
        RUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on iommu=pt"
    systemctl set-default graphical-target  #切换图形界面，换回文本界面是 systemctl set-default multi-user.target

5、安装pve.iso后安装windows的引导  （本人测试未通过，菜单提示签名无效signity invalid）
    https://post.smzdm.com/p/awzzqlep/  实战PVE：N5095 Win+PVE双系统安装，手把手教到会
    d) GRUB复原Windows开机选项
安装完pve后，开机GRUB选项里Windows开机选项会消失，可修改Grub，加入Windows开机选项。

lsblk

确认windows boot efi挂载在哪个sdX，再输入

sudo cfdisk /dev/sdX <-自己的X （无数字）

我的是安装在sdb我的是安装在sdb

把EFI System的UUID记下来把EFI System的UUID记下来

nano /etc/grub.d/40_custom

贴上并填入UUID

menuentry 'Windows 11' {

    search --fs-uuid --no-floppy --set=root <填入UUID>

    chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi

}

实战PVE：N5095 Win+PVE双系统安装，手把手教到会

存档退出

sudo grub-mkconfig -o /boot/grub/grub.cfg

update-grub

重启就可以见到Windows开机选项了

e）



