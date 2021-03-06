微星B250M-E  / B250M迫击炮 OpenCore EFI

### 当前OC版本
0.6.3

### 重要说明 

<font color="red">更新至0.5.7之后，CONFIG文件大改，请务必保存旧的CONFIG文件，默认设置启动项的方法为 呼出启动菜单(win+r),选择对应项, 按 ctrl+enter, 即可设置为默认启动项</font>

<font color="red">CONFIG文件请务必使用XCODE或者ProperTree编辑，请千万不要用Oc Configuretor任何版本进行修改....</font>

### 当前支持

已经可以支持macOS Big Sur 11.0.1 (20B29)

### 机器配置

1. CPU: I5-6500 
2. 内存：金士顿 DDR4 2400 8g 普条 x 2
3. 显卡：HD530(集显)
4. 主板：[微星B250M-E](https://cn.msi.com/Motherboard/B250M-E "官网链接")
   目前已更换为 [B250M迫击炮](https://cn.msi.com/Motherboard/B250M-MORTAR "官网链接")，性质相同
   方法： 
5. 声卡：ALC887(实际上探测为 Realtek ALC888B (0x0887) )，仿冒ID为40  /  迫击炮为ALC889，仿冒ID为1 
6. 硬盘: 雷克沙512M SSD M.2 2280(需升级最新版本BIOS才可识别), 西数1T硬盘
7. 键盘: 达尔优DK100
8. 鼠标: DELL MS 116 
9. 网卡：板载 RTL8111H / TP-LINK TL-WN725N V2 / COMFAST CF-812AC 

### 实现功能

1. 11.0.1 除了快捷键都应该算是OK了
2. SSD已内置，网卡也已内置
3. 4K硬解也已OK
4. 声卡仿冒成功，基本完美识别，可以识别前后也可以识别显示器的HDMI
5. 原生电源管理(节能5项)
6. USB电源管理
7. 加入VirtualSMC的CPU温度传感器，istatus显示正常 (2019-11-25)

### 内核驱动
1. OpenRuntime.efi    核心驱动
2. HFSPlus.efi        支持HFS格式的驱动
3. AudioDxe.efi       开机音乐

### 系统补丁
1. [lilu.kext](https://github.com/acidanthera/OpenCorePkg)   1.4.9
2. [VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC/)  1.1.8
3. [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen) 1.4.4
4. [AppleALC.kext](https://github.com/acidanthera/AppleALC)   1.5.4
5. [IntelMausi](https://github.com/acidanthera/IntelMausi)  1.0.4
6. [RtWlanU.kext + RtWlanU1827.kext](https://github.com/chris1111/Wireless-USB-Adapter-Clover)   无线网卡驱动
7. USBPorts.kext  自己生成 (如果出现U口失灵，删除他自己做)

### DSDT
1. SSDT-EC-USBX.aml   EC控制器
2. SSDT-PLUG.aml  CPU电源管理
3. SSDT-NVME.aml  NVME支持

### 需要自己动手的
1. 因为原生不支持nvram所以需要工具生成，下载完EFI之后还需要用 LogoutHook来生成nvram，不然无法修改启动项，方法请阅读:[https://blog.xjn819.com/post/opencore-guide.html](https://blog.xjn819.com/post/opencore-guide.html) 3.1 这一节，就2句命令，直接照作即可。
2. 暂时没有了

### 非常重要
1. 本EFI已经在BIOS关闭了Fast Boot / CFG Lock / VT-d / CSM，请配合食用，
  （若BIOS里没有CFG LOCK，请升级一下[https://cn.msi.com/Motherboard/support/B250M-E](https://cn.msi.com/Motherboard/support/B250M-E)
**   !!! 刷BIOS有风险，万万不可断电

2. 如果不想升级BIOS，可以阅读[https://blog.xjn819.com/?p=543](https://blog.xjn819.com/?p=543)此文中第2部分CONFIG.PLIST中红字部分即可解决
3. 本包内所含的config.plist中没有三码，请务必添加自己的3码后再进行使用

### 遗留问题

1. HD530的睡眠叫不醒问题！！这个暂时无法解决
2. 一系列的快捷键神马的，我自己用不到就没有加，请自行添加

### 其它说明 

1. 本EFI只适用微星B250M-E，同型号的B250M-F / B250M PRO (包括VHD所有) / B250M NANO 都需要单独仿冒声卡，其它没有什么问题
2. 因为是6代U，所以仿冒的机型为 IMAC17,1，如果修改该值，请配合修改 仿冒的显卡和声卡ID
3. 因为在config.plist中设置了交换command和alt,所以呼出OC菜单为 win+r
4. 其它想好再说

### 对应的工具
1. [Hackintool / 俗称的“瑞士军刀” / https://github.com/headkaze/Hackintool](https://github.com/headkaze/Hackintool)
2. [ProperTree / 好用的plist编辑器 / https://github.com/corpnewt/ProperTree)](https://github.com/corpnewt/ProperTree)
3. [MaciAml / aml编辑工具 / https://github.com/acidanthera/MaciASL)](https://github.com/acidanthera/MaciASL)

### 鸣谢
1. [远景论坛](https://bbs.pcbeta.com, '国内黑苹果基地')
2. [黑果小兵](https://blog.daliansky.net)
3. [XJN](https://blog.xjn819.com)
4. [宪武](https://github.com/daliansky/OC-little)
5. [OPENCORE](https://github.com/acidanthera/OpenCorePkg)
6. [独行秀才](https://shuiyunxc.gitee.io/)