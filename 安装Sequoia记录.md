（整个安装小于1h）

1. 下载镜像：[老吴黑苹果](https://hpglw.com/categories/%E9%95%9C%E5%83%8F/)![](下载镜像.png)

2. 单硬盘多系统 分区方式 参考 [我麦不好](【黑苹果超完整安装教程】https://www.bilibili.com/video/BV1Kj411D7ng?vd_source=a4bc1caacd044a465783d203d0c32784)


2. 制作启动盘

3. 下载EFI文件 并修改。参考[github.com/valnoxy/t480-oc](https://github.com/valnoxy/t480-oc) 修改完成后，将EFI注入到启动盘中

4. 安装 



POST INSTALL
找不到启动项（只能通过启动盘启动）
solution：将启动盘中的EFI复制到前面分区时确定的ESP分区中，然后使用EASYUEFI.EXE添加启动项