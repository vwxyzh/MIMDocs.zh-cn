---
title: "PAM 环境概述 | Microsoft Identity Manager"
description: "查找要成功部署 Privileged Access Management 所需的虚拟机数量和配置"
keywords: 
author: kgremban
manager: femila
ms.date: 07/15/2016
ms.topic: article
ms.prod: identity-manager-2015
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: 479db14c-1bfb-4d7c-a344-cd718a01f328
ms.reviewer: mwahl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ae4c40c73dd9d5860f42e00765a7e34e8ca397a9
ms.openlocfilehash: 3057618c609ed251efe1f6cc6b2d3694ac61eafd


---

# 环境概述

Privileged Access Management 与具有各自分开的驱动器的虚拟机 (VM) 协同工作，这些驱动器在共享网络上相互连接。 可以通过 Windows 8.1、Windows Server 2012 R2 或其他操作系统平台托管这些虚拟机。

![PAM 服务器：关系和支持的平台 - 关系图](media/pam-test-lab-architecture.png)

你将需要至少三个虚拟机。  如果还没有适用于 PAM 管理的 AD 域，则将需要一个额外的虚拟机充当 CORP 域控制器。  如果想要配置 PRIV 软件以实现高可用性，则还需要两个额外的虚拟机。

将存储虚拟机磁盘映像的驱动器需要至少 120 GB 的可用磁盘空间来托管所有虚拟机。  如果打算部署以实现高可用性，请确保磁盘子系统满足 SQL 共享存储的要求。  共享存储可以是 Windows Server 故障转移群集群集磁盘的形式，也可以是存储区域网络 (SAN) 上的磁盘或在 SMB 服务器上的文件共享的形式。 请注意，这些形式只能用于堡垒环境中；建议不要与堡垒环境之外的其他工作负载共享存储，否则可能会损坏堡垒环境的完整性。

> [!NOTE]
> MIM 当前的客户技术预览版 (CTP) 与以前的 CTP 中的数据库或目录内容不兼容。 如果你以前曾为 PAM 或其他方案评估 MIM，请备份并存档用于该测试的虚拟机，并使用以前未用于 MIM 方案的新虚拟机映像启动部署。



<!--HONumber=Jul16_HO3-->


