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

5、



