# ThinkPad T480 安装黑苹果流程

Hi，我是小D。

![Static Badge](https://img.shields.io/badge/%20ThinkPad-T480-blue.svg)![Static Badge](https://img.shields.io/badge/%20macOS-Ventura 13.4.1-brightgreen.svg?logo=apple)![Static Badge](https://img.shields.io/badge/%20OpenCore-0.9.3-blue.svg)



note:此处插入一张黑苹果的截图

**⚠️ 免责声明**

小D对黑苹果并非很懂，只是采用 [@valnoxy](https://github.com/valnoxy/t480-oc?tab=readme-ov-file) 以及 [@我麦不好](https://www.bilibili.com/video/BV1Kj411D7ng/?spm_id_from=333.337.search-card.all.click) 等大佬的安装流程且恰好成功了 。本文出现的所有文件资源若侵权会立刻删掉。

**💻ThinkPad T480硬件信息**

| 类别              | 型号                                                         |
| :---------------- | ------------------------------------------------------------ |
| 主板              | LENOVO 20L5A065CD                                            |
| CPU               | Intel<sup>®</sup> Core™ i5-8250U CPU 1.60GHz                 |
| GPU<sub>1,2</sub> | Intel<sup>®</sup> UHD Graphics 620 128 MB<sub>1</sub> , NVIDIA GeForce MX150 2GB<sub>2</sub> |
| SSD<sub>1,2</sub> | SAMSUNG MZVLB256HAHQ-000L7 256 GB , KBG30ZMT256G TOSHIBA 256 GB |
| Memory            | DDR4 Samsung 2400 MHz                                        |
| WiFi & BT         | Intel<sup>®</sup> Dual Band Wireless-AC 8265                 |



## 1.确定黑苹果安装方式 并进行硬盘分区


 安装方式为`双硬盘双系统`，即将Windows/MacOS分别安装在不同的硬盘上。且对安装的硬盘进行分区。具体的分区操作视频见本仓库。

> 小D的ThinkPad T480硬盘是SAMSUNG MZVLB256HAHQ-000L7，开始尝试在此硬盘上双系统，但安装MacOS的时候跑代码的时候一直报错，后面根据[老吴黑苹果教程](https://hpglw.com/cdc6109c.html)了解到此型号硬盘不可以安装MacOS(具体原理我不懂)，遂加装另一块硬盘KBG30ZMT256G TOSHIBA，将安装方式改为双硬盘双系统

## 2.制作启动盘

2.1 使用黑苹果写入U盘工具![Static Badge](https://img.shields.io/badge/balenaEtcher.exe-green.svg)将MacOS镜像写入u盘，此时得到一个包含默认EFI文件夹的启动盘。具体制作启动盘操作视频见本仓库。

> 小D使用的镜像是`macOS Ventura 13.4 22F66 Installer for OpenCore 0.9.2 and FirPE 1.8.2`，使用u盘至少16G. 

2.2 下载本仓库中的EFI文件夹，修改部分文件，然后替换上一步中启动盘中的默认EFI文件夹。

> [!NOTE]
> 众所周知，EFI文件是黑苹果的灵魂。所以这部分的操作至关重要，它让你的EFI文件变得独一无二

下载本仓库中的<img src="https://img.shields.io/badge/GenSMBIOS.bat-green.svg" >来生成`虚假的苹果设备序列号` , `UUID` and `MLB numbers`.

> The process is the following:
>
> - Download GenSMBIOS as a ZIP, then extract it.
> - Start GenSMBIOS.bat and use option `1` to download MacSerial.
> - Choose option `2`, to select the path of the config.plist file. It will be located in `EFI -> OC` folder.
> - Choose option `3`, and enter `MacBookPro15,2` as the machine type.
> - Press `Q` to quit. Your config now should contain the requied serials.

 找到`EFI -> OC`下面的`config.plist`文件

- add `fake serial number` to your config.plist

- add `the computer's MAC address` to the config.plist file.

- edit `default keyboard layout and language`
- enable / disable `ACPI patches`



<details>
<summary>样例</summary>

</details>

## 3.修改bois的设置

ThinkPad T480开机时一直按住Enter键，即可进入Bios：
- `Security > Security Chip`: must be **Disabled**
- `Memory Protection > Execution Prevention`: must be **Enabled**
- `Virtualization > Intel Virtualization Technology`: must be **Enabled**
- `Virtualization > Intel VT-d Feature`: must be **Enabled**
- `Anti-Theft > Computrace -> Current Setting`: must be **Disabled**
- `Secure Boot > Secure Boot`: must be **Disabled**
- `Intel SGX -> Intel SGX Control`: must be **Disabled**
- `Device Guard`: must be **Disabled**

In Startup menu, set the following options:

- `UEFI/Legacy Boot`: **UEFI Only**
- `CSM Support`: **No**

In Thunderbolt menu, set the following options:

- `Thunderbolt BIOS Assist Mode`: **Disabled**
- `Wake by Thunderbolt(TM) 3`: **No**
- `Security Level`: **No**
- `Support in Pre Boot Environment > Thunderbolt(TM) device`: **No**

Now you can go through the install.




## 4.安装MacOS

4.1 插入启动盘USB,在OpenCore引导的启动界面按`空格键`选择 `"NO NAME (DMG)" or similar`.

> [!NOTE]
> 时间大约为20分钟，请耐心等待

4.2 Wait for the macOS Utilities screen.

4.3 选择Disk Utility工具, 来擦除需要安装的MacOS的硬盘，此时需要擦除的是加装的东芝256G硬盘。命名此盘并 通过 **GUID Partition Map**选择 **APFS**

4.4 擦除之后, 返回 and 返回并选择 **Reinstall macOS** ，接下来按提示操作即可. 整个安装过程大约需要**2 hours**.

> [!NOTE]
> 你的电脑会重启很多次. 确保每次重启都是从启动盘USB.

4.5 一旦你看到 `Region selection` 屏幕, 安装就完成了。

ter