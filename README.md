

<div align="center">

# 🤖 蓝三全向轮步兵机器人 | RoboMaster 开源项目

> *「👋 各位 RoboMaster 同仁、嵌入式与机甲爱好者大家好！
本项目由 RM 老兵倾力打造，低成本全向轮步兵机器人，整机结构、硬件电路、控制代码均完成实机调试。兼顾性价比、实用性与拓展性，既是个人机甲创作、技术研究的优质载体，也是高校战队新人实训、校内新生赛的标准参赛机型。。🤷‍♂️」*
<img width="819" height="700" alt="418d88e12e32344f47547a7d334b8168" src="https://github.com/user-attachments/assets/a8a6ade9-dcee-493b-9e9e-668b12611028" />

<br>

**鲜衣怒马少年郎，意气风发好时光！！！**

**好多学校因为RM机器人太贵经费不足等等诸多原因导致学生没有参加RM的机会，在此开源希望通过最廉价的材料打造最强大的作品**

**希望大家可以一起圆梦！**
<br>

[项目概述](#项目概述) · [结构设计及功能](#🎯二.硬件设计及功能展示) · [声明](#四.开源说明) · [资料下载](https://github.com/buke18/robomaster-soldier-robot/releases#资料包下载)

</div>



## 📋 项目概述
👋 各位 RoboMaster 同仁、嵌入式与机甲爱好者大家好！
本项目由 RM 老兵倾力打造，低成本全向轮步兵机器人，整机结构、硬件电路、控制代码均完成实机调试。兼顾性价比、实用性与拓展性，既是个人机甲创作、技术研究的优质载体，也是高校战队新人实训、校内新生赛的标准参赛机型。

## 🎯一.结构设计

机械结构使用 SolidWorks 完成三维建模与结构设计，主体框架、连接件等常规结构件均采用 3D 打印制作；轮圈外板、装甲外板等外观与受力板材，嘉立创进行 PCB打样，兼顾外观质感与结构强度。

🚀整机动力部件配置如下：

| 功能 | 状态 | 说明 |
|------|------|------|
| 底盘行走 | ✅ | 520 直流编码器电机 |
| 云台俯仰 / 偏航（Pitch/Yaw） | ✅ |4310 无刷电机 |
| 发射摩擦轮 | ✅ | 1806 无刷电机，搭配聚氨酯包胶轮提升摩擦力 |
| 拨弹送弹机构 | ✅ | TT 减速马达 |

<div align=center><img width="691" height="518" alt="image" src="https://github.com/user-attachments/assets/a8a6ade9-dcee-493b-9e9e-668b12611028" />
<div align=left>
  
## 🎯二.硬件设计及功能展示
整套硬件采用模块化分体设计，各功能板独立开发、分工明确，布线简洁、维护方便，同时降低复刻与二次开发难度。

**1.遥控器**
> 主控芯片：STM32F103C8T6
通过 ADC 外设采集摇杆模拟量信号，输入捕获读取编码器数值，配合轮询方式扫描实体按键；整合全部操控指令后，依靠 NRF2401 无线模块向外广播数据。设备搭载双路 NRF2401 无线模块，一路专用于下发遥控指令，另一路负责接收裁判系统数据，实现整机与上位机稳定通信。通过 ADC 外设采集摇杆模拟量信号，输入捕获读取编码器数值，配合轮询方式扫描实体按键；整合全部操控指令后，依靠 NRF2401 无线模块向外广播数据。设备搭载双路 NRF2401 无线模块，一路专用于下发遥控指令，另一路负责接收裁判系统数据，实现整机与上位机稳定通信。

<div align=center><img width="691" height="332" alt="image" src="https://github.com/user-attachments/assets/f8b274f4-7ff9-400c-ba85-44c9dac76581" />
<div align=center><img width="691" height="518" alt="image" src="https://github.com/user-attachments/assets/4ddbdba4-b732-43e4-83d1-62fa985c9beb" />
<div align=left>
  
**2.云台主控**

> 主控芯片：STM32F407VET6
板载 BMI055 六轴陀螺仪、IST8310 三轴磁力计，完成高精度姿态解算；通过 NRF2401 接收遥控器指令，实现云台姿态与位置闭环控制。主控板与 Pitch 轴无刷电机之间采用串口协议通信，数据传输稳定可靠。板载 BMI055 六轴陀螺仪、IST8310 三轴磁力计，完成高精度姿态解算；通过 NRF2401 接收遥控器指令，实现云台姿态与位置闭环控制。主控板与 Pitch 轴无刷电机之间采用串口协议通信，数据传输稳定可靠。
<div align=center><img width="691" height="346" alt="image" src="https://github.com/user-attachments/assets/e9dccfb7-7fca-477d-a884-cc6704cec30b" />
<div align=center><img width="692" height="343" alt="image" src="https://github.com/user-attachments/assets/f5fb34c4-938c-4499-8b53-a693d66b7191" />
<div align=left>

**3.底盘主控**
> 主控芯片：STM32F407VET6
硬件配置、姿态解算方案与云台主控保持一致，依托 NRF2401 无线模块接收遥控指令，完成底盘运动与姿态闭环控制。主控板与 Yaw 轴无刷电机通过串口进行数据交互，协同实现全向移动与云台联动。硬件配置、姿态解算方案与云台主控保持一致，依托 NRF2401 无线模块接收遥控指令，完成底盘运动与姿态闭环控制。主控板与 Yaw 轴无刷电机通过串口进行数据交互，协同实现全向移动与云台联动。
<div align=center><img width="692" height="519" alt="image" src="https://github.com/user-attachments/assets/94f0daa6-0752-4d6f-b2e7-53b55ff1220e" />
<div align=center><img width="693" height="335" alt="image" src="https://github.com/user-attachments/assets/b5dd0aca-8fd4-4ee4-9127-4e9febdf1a10" />
<div align=left>

**4.发射机构控制板**
> 主控芯片：STM32F103C8T6
板载多路驱动外设，功能划分清晰：输出四路 PWM 信号驱动电调，精准控制摩擦轮转速；单路 PWM 控制发射灯条灯光效果；集成 TB6612 直流电机驱动芯片，驱动 TT 马达运转，灵活调节拨弹盘送弹速度。板载多路驱动外设，功能划分清晰：输出四路 PWM 信号驱动电调，精准控制摩擦轮转速；单路 PWM 控制发射灯条灯光效果；集成 TB6612 直流电机驱动芯片，驱动 TT 马达运转，灵活调节拨弹盘送弹速度。
<div align=center><img width="692" height="519" alt="image" src="https://github.com/user-attachments/assets/51affd6d-3243-401d-a7a0-48cc97b29c85" />
<div align=center><img width="691" height="518" alt="image" src="https://github.com/user-attachments/assets/9217e6c9-f2b5-462f-9fd6-3d345b8205a5" />
<div align=left>

**5.裁判系统控制板**
> 主控芯片：STM32F103C8T6
专负责整机裁判系统相关功能，包含装甲灯效控制、击打检测、血量统计三大核心功能。每块装甲板四角搭载微动开关，通过读取 IO 口电平变化识别击打状态、累计击打次数，并将数据回传至遥控器，配合上位机完成实时血量统计。可编程灯效，可高度复刻标准 RM 装甲板灯光逻辑。专负责整机裁判系统相关功能，包含装甲灯效控制、击打检测、血量统计三大核心功能。每块装甲板四角搭载微动开关，通过读取 IO 口电平变化识别击打状态、累计击打次数，并将数据回传至遥控器，配合上位机完成实时血量统计。可编程灯效，可高度复刻标准 RM 装甲板灯光逻辑。
<div align=center><img width="692" height="339" alt="image" src="https://github.com/user-attachments/assets/8accd376-5182-416d-b56d-455aef70822b" />
<div align=center><img width="692" height="365" alt="image" src="https://github.com/user-attachments/assets/9ad5b520-5172-46b1-924c-8eea80fbd56a" />
<div align=left>

**6.无刷电机控制板**
> 采用成熟的 FOC 磁场定向控制 方案，主控为 STM32F103C8T6，外围搭配 DRV8313 三相驱动芯片、INA240 高精度电流采样芯片、AS5600 磁电角度传感器。
目前已完整开发电流环、速度环、位置环三闭环控制代码，电机默认工作在位置 + 速度双闭环模式，运行平稳、定位精准。目前已完整开发电流环、速度环、位置环三闭环控制代码，电机默认工作在位置 + 速度双闭环模式，运行平稳、定位精准。
<div align=center><img width="692" height="514" alt="image" src="https://github.com/user-attachments/assets/9c988c98-6a5c-4a08-9b83-c08ea91ef990" />
<div align=center><img width="691" height="274" alt="image" src="https://github.com/user-attachments/assets/4ddde1e7-b944-46b4-8555-3f8fe1ea9f6b" />
<div align=left>

**7.装甲板传感器**
> 灯效部分采用多颗 WS2812B 串行级联，支持多彩动态灯光自定义；装甲四角集成微动开关，模块受撞击时输出高电平信号，为击打检测提供硬件支撑。
<div align=center><img width="692" height="395" alt="image" src="https://github.com/user-attachments/assets/815e4af6-cd0b-493e-af45-0c4043c7e633" />
<div align=center><img width="692" height="566" alt="image" src="https://github.com/user-attachments/assets/0c6ca532-5928-409c-93a1-52c7bfe13cf6" />
<div align=left>

**8.十轴传感器**
> 集成多款高性能传感芯片：BMI055 六轴陀螺仪加速度计、IST8310 三轴磁力计、BMP280 气压传感器，所有器件均通过 IIC 总线完成通信与数据读取，集成度高、体积小巧。
<div align=center><img width="692" height="376" alt="image" src="https://github.com/user-attachments/assets/2251f897-a23f-4a0a-b5ca-c8065575216f" />
<div align=left>
  
**9.分电板**
> 整机电源分配专用板卡，实现多路电压输出、为所有主控、电机、传感器稳定供电。
<div align=center><img width="650" height="617" alt="image" src="https://github.com/user-attachments/assets/762a6814-b3c0-4cbb-8076-40ba270aa3b9" />
<div align=left>

**10.发射灯条**
> 独立式发射机构氛围灯条，由主控板 PWM 驱动，可实现常亮、频闪、爆闪，流水灯等多种灯光效果。
<div align=center><img width="691" height="506" alt="image" src="https://github.com/user-attachments/assets/72b74997-064e-4967-a137-cfbfbd21eb30" />
<div align=left>

## 三.操作介绍
整机操控逻辑参照穿越机设计，上手门槛低、操控手感流畅，轻推摇杆即可完成机器人移动、云台瞄准、弹药发射等全部动作。
<div align=center><img width="692" height="374" alt="image" src="https://github.com/user-attachments/assets/fdbec25c-c9b2-4f85-83c0-b0afc08984e5" />
<div align=left>

整套程序采用模块化分层开发，逻辑清晰、耦合度低，便于调试与功能拓展，下图为项目整体软件架构：
<div align=center><img width="692" height="401" alt="image" src="https://github.com/user-attachments/assets/c6005652-7dea-4a67-9b6c-64492c6d1e8d" />
<div align=left>
  
## 四.开源说明
本项目为全开源项目，面向所有 RoboMaster 爱好者、在校战队、嵌入式开发者免费开放，所有资料仅供学习、交流、非商业用途使用。
[资料下载](https://github.com/buke18/robomaster-soldier-robot/releases#资料包下载)
**1.结构文件**
3D 模型区已上传通用 .stl 白模文件，可直接用于 3D 打印；完整 SolidWorks 工程、带贴图高精度模型因体积超出平台限制，下载后即可使用。解压时请保留原有文件目录，避免贴图、资源加载异常。

**2.硬件资料**
## 包含全模块原理图、PCB 源文件、完整 BOM 清单，参数标注齐全，可直接打样复刻。因为文件过大，且不易整理，分为四部分上传至Releases中，并添加了4个TAG对应四个部分！

**3.程序代码**
基于 STM32 HAL库+freertos开发，代码注释详实、模块化划分清晰，支持二次修改与功能拓展，适合入门学习与进阶开发。

**4.使用规范**
总复刻成本在900元RMB-1500元左右！
## 欢迎大家交流探讨、学习借鉴；二次转发、改编使用时，请保留原项目出处。
