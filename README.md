# ZSWatch 中文说明与学习实践

ZSWatch 是一个开源智能手表项目，包含硬件设计和固件。固件主要使用 C 语言编写，基于 Zephyr 实时操作系统，界面使用 LVGL，主控芯片为 Nordic nRF5340。

本仓库是 [ZSWatch/ZSWatch](https://github.com/ZSWatch/ZSWatch) 的 Fork（保留原项目来源的副本），保留上游源码、提交历史、版权和许可证。个人学习与扩展由 [h990566354-sudo](https://github.com/h990566354-sudo) 按阶段推进。

本 README 根据[上游英文说明](https://github.com/ZSWatch/ZSWatch/blob/1d4ad702b5d0242895c409243d4e189f287f9104/README.md)译写，并补充中文学习入口。下方项目功能描述来自上游，不代表个人已经实现了这些功能。

## 从这里开始学习

**[打开中文学习资料首页](docs/zh-learning/00-开始阅读.md)**

| 内容 | 阅读入口 |
| --- | --- |
| 项目是什么、第一课怎样读 About 应用 | [项目全貌与第一课](docs/zh-learning/01-项目全貌与第一课.md) |
| 启动、界面、蓝牙、传感器等模块怎样连接 | [源码导读](docs/zh-learning/02-源码导读.md) |
| 开发工具、编译和模拟器运行方式 | [环境与运行](docs/zh-learning/03-环境与运行.md) |
| 动手练习、个人扩展与简历证据 | [学习任务与简历证据](docs/zh-learning/04-学习任务与简历证据.md) |
| GitHub 仓库管理与学习进度 | [GitHub 与进度](docs/zh-learning/05-GitHub与进度.md) |

资料包含 Codex 辅助整理的分析，需要结合源码和动手验证学习。

**当前个人进度：** 已建立 Fork 并整理中文学习资料；尚未完成本人的编译运行、个人功能开发或实机验证。后续根据真实改动和验证结果更新成果。

第一课从 [About 应用目录](app/src/applications/about/)开始。About 是手表中的“关于”页面，用于显示板卡信息、固件版本、编译时间和应用数量等信息：

- [about_app.c](app/src/applications/about/about_app.c)：应用注册、打开、关闭及信息整理。
- [about_ui.c](app/src/applications/about/about_ui.c)：界面的文字、图片和布局。
- [about_ui.h](app/src/applications/about/about_ui.h)：界面函数声明。
- [CMakeLists.txt](app/src/applications/about/CMakeLists.txt)：把该目录的源码加入编译。

## 项目介绍

官方网站：[zswatch.dev](https://zswatch.dev/)

<img alt="ZSWatch 项目标志" src="https://github.com/user-attachments/assets/6669a8eb-a4fd-424e-9a7c-201e0a571641" />

<div align="center">

[![许可证](https://img.shields.io/badge/%E8%AE%B8%E5%8F%AF%E8%AF%81-GPL%203.0-blue.svg)](https://opensource.org/licenses/GPL-3.0)
[![社区](https://img.shields.io/badge/%E7%A4%BE%E5%8C%BA-Discord-blue?logo=discord&logoColor=white)](https://discord.gg/8XfNBmDfbY)
[![文档](https://img.shields.io/badge/%E6%96%87%E6%A1%A3-zswatch.dev-green)](https://zswatch.dev/docs/intro)

<p float="left">
<img alt="佩戴中的 ZSWatch" src=".github/images/in_use.jpg" width="67.5%" object-fit="cover"/>
<img alt="透明树脂外壳的 ZSWatch" src=".github/images/v3_case.jpg" width="31%" object-fit="cover"/>
</p>
<sub>
  左图：ZSWatch v4 的 CNC 加工不锈钢外壳；右图：透明树脂 3D 打印外壳。
</sub>
</div>

原项目从零设计了智能手表的硬件和软件，基于 [Zephyr 项目](https://www.zephyrproject.org/)的实时操作系统，因此命名为 **ZSWatch**，即 *Zephyr Smartwatch*（Zephyr 智能手表）。

**WatchDK** 是 ZSWatch 的开发套件，采用与最终手表相同的 nRF5340 芯片及传感器。它的体积更大，便于开发和调试，可通过 USB-C 供电，电池为可选项。上游英文说明中的标价为 99 美元，实际售价以[购买页面](https://www.elecrow.com/zswatch-development-kit.html)为准。

- [WatchDK 购买页面](https://www.elecrow.com/zswatch-development-kit.html)
- [WatchDK 官方快速入门](https://zswatch.dev/docs/getting-started/watchdk-quickstart)

<kbd><img title="ZSWatch 开发套件" src="website/blog/2025-12-05-dk-and-hr/watchdk.jpg" alt="ZSWatch 开发套件展示图"/></kbd>

<sub>ZSWatch 开发套件（WatchDK）</sub>

https://github.com/ZSWatch/ZSWatch/assets/4318648/ec1a94fd-a682-4559-9e68-f3e5bfcbe682

## 官方文档

完整的官方文档位于 **[zswatch.dev](https://zswatch.dev)**。以下链接主要是英文资料，可以配合本仓库的中文学习资料阅读：

- [快速入门](https://zswatch.dev/docs/getting-started/watchdk-quickstart)：WatchDK 的首次使用指南。
- [工具链、编译与烧录](https://zswatch.dev/docs/development/toolchain)：安装开发环境，把源码编译为固件，再写入设备。
- [编写应用](https://zswatch.dev/docs/development/writing_apps)：怎样为 ZSWatch 创建新的应用。
- [硬件设计](https://zswatch.dev/docs/hardware-design)：电路板设计说明。

## 项目功能

### 硬件

以下内容对应上游说明中的硬件设计，具体器件应结合目标板版本核对。

- [nRF5340](https://www.nordicsemi.com/Products/nRF5340) 低功耗蓝牙芯片，使用 [u-blox NORA-B10 模块](https://www.u-blox.com/en/product/nora-b1-series-open-cpu)。
  - 双核架构，应用核心最高运行频率为 128 MHz。
  - 应用核心配有 512 KB RAM 和 1 MB Flash。
  - 屏幕通过 30 MHz SPI 接口连接。
- [240 × 240 像素圆形显示屏](https://www.buydisplay.com/catalog/product/view/id/1849/s/240x240-round-ips-tft-lcd-display-1-28-capacitive-touch-circle-screen/)，支持触摸操作。
- Bosch [BMI270](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bmi270-ds000.pdf) 惯性测量单元（IMU），用于手势操作、抬腕唤醒和计步。
- Bosch [BMP581](https://www.bosch-sensortec.com/products/environmental-sensors/pressure-sensors/bmp581/) 高性能气压传感器；上游说明给出的高度测量精度约为 20 cm。
- ST [LIS2MDLTR](https://www.st.com/resource/en/datasheet/lis2mdl.pdf) 磁力计，用于测量磁场。
- Macronix [MX25U51245GZ4I00](https://www.mouser.de/datasheet/2/819/MX25U51245G_2c_1_8V_2c_512Mb_2c_v1_4-3371129.pdf) 外部 Flash，容量为 64 MB。
- Broadcom [APDS-9306-065](https://docs.broadcom.com/docs/AV02-4755EN) 光照传感器，用于自动调节屏幕亮度。
- Micro Crystal [RV-8263-C8](https://www.microcrystal.com/en/products/real-time-clock-rtc-modules/rv-8263-c8) 实时时钟（RTC），用于计时和闹钟功能。
- Knowles [SPK0641HT4H-1](https://www.knowles.com/docs/default-source/model-downloads/spk0641ht4h-1-rev-a.pdf) I2S 麦克风，用于录音。
- Nordic [nPM1300](https://docs.nordicsemi.com/category/npm1300-category) 电源管理芯片（PMIC），用于电源和系统管理。
- 扬声器，需要搭配健康与音频扩展板。

### 电路板设计

硬件使用 KiCad 设计，相关仓库包括：

- [手表电路板](https://github.com/ZSWatch/Watch-HW)：直径约 38 mm 的手表电路板。
- [开发套件电路板](https://github.com/ZSWatch/Watch-DevKit-HW)：尺寸更大，带有引出排针和调试接口。
- [扩展电路板](https://github.com/ZSWatch/Extension-HW)：健康监测和音频功能扩展。
- [底座与接口引出板](https://github.com/ZSWatch/Dock-HW)：通过 USB-C 引出调试器和串口（UART）连接。

<kbd><img title="v5 硬件概览（上游原图标注 v6 即将推出）" src="resources/images/Hardware-Overview.png" alt="ZSWatch v5 硬件概览"/></kbd>

### 健康与音频扩展板（开发中）

这是一块直径约 16.8 mm 的小型扩展板，可以插接到 WatchDK 的排针上。上游说明将其标为开发中，设计、物料清单（BOM）和固件支持仍可能调整。

相关背景和进度文章：

- [开发套件与健康扩展板集成](https://zswatch.dev/blog/dk-and-hr-integration)
- [硬件、外部存储执行与 USB 供电进度](https://zswatch.dev/blog/progress-hw-xip-usb-power)
- [心率功能与无线固件升级进度](https://zswatch.dev/blog/progress-hr-fota)

主要器件：

- Analog Devices / Maxim `MAX86141` 光学模拟前端，搭配 ams OSRAM `SFH 7016` RGB/红外 LED 模块和 Vishay `VEMD8082` 光电二极管。
- Analog Devices / Maxim `MAX32664` 生物识别传感器处理芯片。
- Renesas / Dialog `DA7212` 音频编解码芯片，用于扬声器支持。
- Amphenol `101P014FB110` 板对板连接器。

### 软件

- 通过低功耗蓝牙（BLE），与 [ZSWatch 手机配套应用](https://zswatch.dev/docs/getting-started/companion_app)（iOS / Android）或 [GadgetBridge](https://codeberg.org/Freeyourgadget/Gadgetbridge)（Android）通信。
- 支持动态切换多个表盘，显示时间、日期、电量、天气、步数、通知和环境数据等。
- 支持弹出通知。
- 提供应用选择界面和可扩展的应用框架，包括[设置](app/src/applications/settings/)、[音乐控制](app/src/applications/music_control/)、[指南针](app/src/applications/compass/)等应用。
- 支持计步、手势操作等功能。

手表也支持 [Felix Biego](https://github.com/fbiego) 制作的 ESP32 表盘，详见[相关表盘仓库](https://github.com/Kampi/esp32-lvgl-watchface)。

### 与手机连接

以下方式依据上游说明整理，具体安装和接入步骤请参考[官方手机连接指南](https://zswatch.dev/docs/getting-started/phone_setup)。

**iOS：** 上游推荐使用 App Store 中的官方 [ZSWatch 手机配套应用](https://apps.apple.com/us/app/zswatch/id6759058602)。ZSWatch 还支持苹果原生的[通知中心服务（ANCS）](https://developer.apple.com/library/archive/documentation/CoreBluetooth/Reference/AppleNotificationCenterServiceSpecification/Specification/Specification.html)和[媒体服务（AMS）](https://developer.apple.com/library/archive/documentation/CoreBluetooth/Reference/AppleMediaService_Reference/Specification/Specification.html)。

**Android：** 上游说明将配套应用标为实验阶段，需要邀请才能使用，可通过 [Discord](https://discord.gg/8XfNBmDfbY) 或[上游联系邮箱](mailto:mail@zswatch.dev)申请。上游建议希望获得稳定体验的用户使用 [GadgetBridge](https://codeberg.org/Freeyourgadget/Gadgetbridge)。

### 外壳

支持 3D 打印外壳和按钮，也提供 CNC 加工金属外壳的方案。

## 获取开发套件或自行制作

**用于开发和调试：** 上游推荐从 [WatchDK 开发套件](https://zswatch.dev/docs/getting-started/watchdk-quickstart)开始。它采用与最终手表相同的 nRF5340、传感器和显示屏，提供引出排针、带 SWD / UART 连接的 USB-C 接口、电流测量排针及调试接口。套件不包含电池，电池可以按需选用。

购买入口：[Elecrow 的 WatchDK 页面](https://www.elecrow.com/zswatch-development-kit.html)。

**自行制作：** 可以到前述硬件仓库查看设计和订购信息。上游说明中的最终小型手表硬件仍在开发。

## 演示

- [通过 GadgetBridge 和 BLE 转发 HTTP 请求](https://github.com/ZSWatch/ZSWatch/assets/4318648/12d6e754-ceb3-4efd-9a75-d207aaeb0e82)
- [表盘演示](https://github.com/ZSWatch/ZSWatch/assets/4318648/13e43401-1c00-40ab-866f-e6518e61940d)

## 开发入门

开发环境配置、编译和烧录步骤见[官方工具链与构建指南](https://zswatch.dev/docs/development/toolchain)。编写新应用见[官方应用开发说明](https://zswatch.dev/docs/development/writing_apps)。

Windows 可以搭建工具链并编译真实硬件的固件。要在电脑上运行官方界面模拟器，需要 Linux 环境；Windows 用户可通过 WSL2 或 Linux 虚拟机使用它。具体步骤见[官方模拟器说明](https://zswatch.dev/docs/development/linux_development)和本仓库的[中文环境与运行指南](docs/zh-learning/03-环境与运行.md)。

建议学习顺序：读懂 About 应用 → 配置开发环境并编译运行 → 修改一处界面文字并验证 → 开发一个个人小功能 → 记录修改和测试结果。

## 许可证：GPL-3.0

本项目沿用上游的 GPL-3.0 许可证，完整条款见仓库中的 [LICENCE](LICENCE)。

原作者在上游说明中表达的初衷是：希望基于项目继续开发的人也开源分享改进，让大家受益；关于许可证的意见可以与上游项目沟通。本仓库保留原项目的版权和许可证。

## 致谢

### 资金支持

原项目获得了 [NGI0 Commons Fund](https://nlnet.nl/commonsfund) 的部分资助。该基金由 [NLnet](https://nlnet.nl) 设立，并得到欧盟委员会[下一代互联网（NGI）计划](https://ngi.eu)的资金支持。详情见 [NLnet 的 ZSWatch 项目页面](https://nlnet.nl/project/ZSWatch)。

[<img src="https://nlnet.nl/logo/banner.png" alt="NLnet 基金会标志" width="20%" />](https://nlnet.nl)
[<img src="https://nlnet.nl/image/logos/NGI0_tag.svg" alt="NGI Zero 标志" width="20%" />](https://nlnet.nl/commonsfund)

### 项目支持

<p align="left">
  <a href="https://www.pcbway.com/">
    <img width="20%" src=".github/images/pcbway_logo.svg" alt="PCBWay 标志" style="vertical-align:middle;" />
  </a>
  <a href="https://www.segger.com/">
    <img width="20%" src=".github/images/SEGGER-Logo-the-embedded-experts-RGB.jpg" alt="SEGGER 标志" style="vertical-align:middle; margin-right: 32px;" />
  </a>
</p>

感谢 **PCBWay** 赞助原型电路板的制造和组装。上游项目推荐 PCBWay 提供 ZSWatch 电路板制造及组装服务。

## 更多资料

- [原作者在 2023 年 Zephyr 开发者峰会上的演讲](https://www.youtube.com/watch?v=MmCzV0jV9hs)
