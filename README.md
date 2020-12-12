# CVN B460I GAMING V20 Hackintosh OpenCore

## 配置

|          |                  |
| -------- | ---------------- |
| CPU      | I5 10400         |
| GPU      | UHD630           |
| WIFI     | AX200            |
| RAM      | 32GB*2           |
| OpenCore | v0.63-release    |
| macOS    | Catalina 10.15.7 |

## Bios

| 设置                             | 设置 |
| -------------------------------- | ---- |
| 高级模式->高级->C状态            | 关闭 |
| 高级模式->高级->CSM支持          | 关闭 |
| 高级模式->高级->超线程           | 启动 |
| 高级模式->高级->英特尔虚拟化技术 | 启动 |
| 高级模式->高级->XHCI交接         | 启动 |
| 高级模式->高级->SATA模式         | AHCI |
| 高级模式->主板芯片组->ME控制     | 关闭 |
| 高级模式->引导->Bios写保护       | 关闭 |

## SMBIOS

`MLB`，`SystemSerialNumber`，`SystemUUID`请自己通过[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)生成后填充到`config.plist`里。

## Issue

1.HDMI输出4K会紫屏。

2.USB未定制，可以参考黑果小兵教程定制。

3.屏蔽了独显。因为目前我用不上。

## 开机操作

开机后啥也不按，默认进入`Windows`系统，这是真正的`Windows`，会正常认出所有硬件的原始信息，独立显卡也正常使用。
开机后如果狂按F11，会有`Windows Boot Manager`和`OpenCore`两个引导项，选`Windows Boot Manager`还是上面说说的真正`Windows`。选择`OpenCore`就可以进入`Mac`的引导界面。
需要注意的是,`OpenCore`里的`Windows`会让Windows认为自己运行在`Mac`上,同理独立显卡也不会工作（被`OpenCore`屏蔽了）。
开机后如果按`Enter`会进入`bios`，如果进入后卡A9或者B9，那就先进入`OpenCore`里，选择`Reset Nvram`即可，但这样似乎会清空引导项，一般不推荐你进`bios`改设置
`bios`里的`igfx`显存配置请保持为`128MB`和`MAX`。

## 引导编辑

使用`bootice`编辑

`mac`和`windows`共用一个600MB大小的`EFI`分区，也叫`ESP`分区，600MB是我分的，`windows`默认创建是100MB，不满足`mac`的200MB要求。

`bootice`里面引导顺序调整在`uefi`页面

`bootice`里物理磁盘-分区管理，把ESP分区显现出来并分配盘符，就可以在`UEFI`里的`修改启动序列`里添加`引导`指向ESP分区里面的efi文件。
