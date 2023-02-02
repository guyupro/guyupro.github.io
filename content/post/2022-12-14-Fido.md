---
title: "Fido 开源PowerShell脚本下载windows原版镜像ISO"
date: 2022-12-14
tags: ["PowerShell"]
draft: false
---

项目地址：<https://github.com/pbatard/Fido>

```
PS C:\Projects\Fido> .\Fido.ps1 -Win 10
No release specified (-Rel). Defaulting to '21H1 (Build 19043.985 - 2021.05)'.
No edition specified (-Ed). Defaulting to 'Windows 10 Home/Pro'.
No language specified (-Lang). Defaulting to 'English International'.
No architecture specified (-Arch). Defaulting to 'x64'.
Selected: Windows 10 21H1 (Build 19043.985 - 2021.05), Home/Pro, English International, x64
Downloading 'Win10_21H1_EnglishInternational_x64.iso' (5.0 GB)...
PS C:\Projects\Fido> .\Fido.ps1 -Win 10 -Rel List
Please select a Windows Release (-Rel) for Windows 10 (or use 'Latest' for most recent):
 - 21H1 (Build 19043.985 - 2021.05)
 - 20H2 (Build 19042.631 - 2020.12)
 - 20H2 (Build 19042.508 - 2020.10)
 - 20H1 (Build 19041.264 - 2020.05)
 - 19H2 (Build 18363.418 - 2019.11)
 - 19H1 (Build 18362.356 - 2019.09)
 - 19H1 (Build 18362.30 - 2019.05)
 - 1809 R2 (Build 17763.107 - 2018.10)
 - 1809 R1 (Build 17763.1 - 2018.09)
 - 1803 (Build 17134.1 - 2018.04)
 - 1709 (Build 16299.15 - 2017.09)
 - 1703 [Redstone 2] (Build 15063.0 - 2017.03)
 - 1607 [Redstone 1] (Build 14393.0 - 2016.07)
 - 1511 R3 [Threshold 2] (Build 10586.164 - 2016.04)
 - 1511 R2 [Threshold 2] (Build 10586.104 - 2016.02)
 - 1511 R1 [Threshold 2] (Build 10586.0 - 2015.11)
 - 1507 [Threshold 1] (Build 10240.16384 - 2015.07)
PS C:\Projects\Fido> .\Fido.ps1 -Win 10 -Rel 20H2 -Ed Edu -Lang Fre -Arch x86 -GetUrl
https://software-download.microsoft.com/db/Win10_Edu_20H2_v2_French_x32.iso?t=c48b32d3-4cf3-46f3-a8ad-6dd9568ff4eb&e=1629113408&h=659cdd60399584c5dc1d267957924fbd
```