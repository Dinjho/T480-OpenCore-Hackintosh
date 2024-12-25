# ThinkPad T480 安装黑苹果流程


##### ⚠️ 免责声明
作为业余爱好者，小D对黑苹果并非很懂，只是采用 [@valnoxy](https://github.com/valnoxy/t480-oc?tab=readme-ov-file) 以及 @[我麦不好](https://www.bilibili.com/video/BV1Kj411D7ngvd_source=8fdb5ed5c412c5331312054106d1b6df) 等大佬的安装流程且恰好成功了。




####1.确定黑苹果安装方式 并进行硬盘分区
	
 使用的安装方式为`双硬盘双系统`，即将windows/macos安装在不同的硬盘上
> 本人的硬盘是三星xxxx，开始几次的安装都是单硬盘双系统，但是安装macos的时候跑代码的时候一直报错，后面根据[老吴黑苹果教程](https://hpglw.com/cdc6109c.html)了解到此型号硬盘不可以安装macos，后面才将安装方式改为双硬盘双系统

####2.制作启动盘

2.1 使用balenaEtcher将macos镜像写入u盘，此时得到一个包含默认efi文件夹的启动盘。

2.2 下载efi，替换上一步中启动盘中的默认efi文件夹。
> 稍等，替换之前先修改`EFI -> OC`下面的config.plist文件内的 GenSMBIOS
MAC address keyboard layout and language ACPI patches 等选项


####3.修改bois的设置
####4.安装macOS