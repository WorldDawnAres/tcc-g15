# 目录

**[English](README_en.md) | [简体中文](README.md)**

- [戴尔 G15 等机型的 Thermal Control Center（温控中心）](#戴尔-g15-等机型的-thermal-control-center温控中心)
- [目标平台](#目标平台)
- [功能介绍](#功能介绍)
- [界面提示](#界面提示)
- [已知限制](#已知限制)
- [为什么 AWCC 很糟糕](#为什么-awcc-很糟糕)
- [工作原理](#工作原理)
- [如何从源码运行](#如何从源码运行)
- [关于 AWCC 的遥测行为](#关于-awcc-的遥测行为)
- [致谢](#致谢)
- [更新日志](#更新日志)
- [许可证](#许可证)

## 戴尔 G15 等机型的 Thermal Control Center（温控中心）

一款开源的 AWCC 替代方案

[点击此处下载](https://github.com/WorldDawnAres/tcc-g15/releases)  
*注意：本应用需要管理员权限运行*

![Screenshot 1](./screen-1.png "截图1")
![Screenshot 1](./screen-2.png "截图2")

> 喜欢这个工具？很高兴它帮到你了！😸 欢迎分享给更多人 🚀 并为项目点个 Star ⭐  
> 如果你遇到问题，请通过[创建 issue](https://github.com/AlexIII/tcc-g15/issues) 来报告。我们非常欢迎你的反馈！

**AWCC - Alienware Command Center，是戴尔 G 系列笔记本出厂预装的一个控制温度的工具，但它有许多问题。*

## 目标平台

操作系统：Windows 10 / 11

支持的笔记本型号 (据用户反馈)：

- Dell G15: 5511、5515、5520、5525、5530、5535、5590
- Alienware m16 R1
- Dell G3 3590, G3 15 3500
- Dell Alienware 16X Aurora

> 其他 G15 或 Alienware 型号也有可能支持。  
> 如果你成功运行或遇到问题，请反馈给我们。

## 功能介绍

- ✔️ 切换温控模式（G 模式、平衡、自定义）
- ✔️ 显示 GPU / CPU 温度及风扇转速
- ✔️ 半手动控制风扇转速
- ✔️ 支持高温时自动启用 G 模式
- ✔️ 支持键盘上的 G 模式快捷键

## 界面提示

- 托盘图标角落的白点表示当前 G 模式状态：

    ![Screenshot 1](./g_off.png "g_off")  G 模式关闭  ![Screenshot 1](./g_on.png "g_on") G 模式开启

- 将鼠标悬停在界面元素上可以查看提示说明。

## 已知限制

- 需要管理员权限运行（为了访问 WMI 接口）
- 手动风扇控制并非完全手动。若设定转速太低，BIOS 会在温度过高时强制提高风扇转速，以防止过热。
- **“开机自启”功能可能无法在部分系统中正常工作。** 它通过添加计划任务来实现启动，但有些系统的安全策略可能会阻止该任务运行。可以尝试其他方式实现自启。[参考这个 Issue](https://github.com/AlexIII/tcc-g15/issues/7)
- 某些极少情况下，驱动可能会报告错误的 GPU 温度。[相关问题](https://github.com/AlexIII/tcc-g15/issues/9)
- 在切换至 G 模式或从 G 模式切换回来时，**可能会造成 1 秒左右的全系统卡顿**。这是戴尔接口本身的问题，无法修复。如不希望自动切换 G 模式，请关闭故障保护功能。

## 为什么 AWCC 很糟糕

- ❌ AWCC 没有切换 G 模式的按钮
- ❌ AWCC 的手动风扇控制功能目前是坏的
- ❌ AWCC 臃肿、卡顿、界面杂乱，却连最基本功能都处理不好
- ❌ [AWCC 会进行隐私追踪](#关于-awcc-的遥测行为)
- ❌ AWCC 经常随机崩溃并生成错误报告

如果这个替代方案对你有效，可以安全卸载：

- Alienware CC Components  
- Alienware Command Center Suite  
- Alienware OC Controls  

## 工作原理

本项目基于 PyQt 构建图形界面，通过访问 Dell 的 WMI 温控接口工作。

关于该接口的探索与说明文档，请查看：[WMI-AWCC-doc.md](WMI-AWCC-doc.md)

## 如何从源码运行

```bash
python3 -m pip install -r ./requirements.txt
python3 src\\tcc-g15.py
```

## 关于 AWCC 的遥测行为

考虑到我们当前所处的时代，我知道这可能不会让任何人感到惊讶

AWCC会默默发送一些遥测数据，且用户无法选择退出。

它会发送数据到以下地址：

```bash
https://tm-sdk.platinumai.net
https://qa-external-tm.plawebsvc01.net
```

## 致谢

特别感谢以下为项目做出贡献的人们：

- @AprDeci - 新功能与代码支持
- @T7imal, @cemkaya-mpi, @THSLP13, @Terryxtl - 测试与调试
- @Dtwpurple, @WinterholdPrime, @Dhia-zorai, @fraPCI - 兼容性报告

## 更新日志

- 1.6.5
  - 更新依赖（开发）
  - 更新导入结构（开发）
  - 修复：处理不兼容的模式设置（开发）

- 1.6.4
  - 修复：不再限制显示的 RPM 值

- 1.6.3
  - 托盘图标显示温度、风扇转速、当前模式
  - 托盘图标显示 G 模式状态
  - 支持从托盘菜单切换温控模式
  - 修复高分屏托盘图标模糊问题
  - 启动速度更快

- 1.6.2
  - 显示 GPU/CPU 型号（修复自 1.6.1）
  - 小错误修复

- 1.6.0
  - 支持键盘快捷键控制 G 模式

- 1.5.4
  - 修复异常退出（如关机）时未保存设置的问题
  - 修复恢复默认设置的逻辑

- 1.5.3
  - 增加故障保护触发延迟，防止温度尖峰导致频繁切换

## 许可证

© github.com/AlexIII

本项目基于 GPL v3 开源许可证发布。
