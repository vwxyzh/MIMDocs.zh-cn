---
title: "PAM 环境层模型 | Microsoft Identity Manager"
description: "了解基于对风险的承受程度分离系统的层模型。"
keywords: 
author: kgremban
manager: femila
ms.date: 07/15/2016
ms.topic: article
ms.prod: identity-manager-2015
ms.service: microsoft-identity-manager
ms.technology: active-directory-domain-services
ms.assetid: c6e3cd02-1e32-4194-a8ed-3a0b3d022a43
ms.reviewer: mwahl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ae4c40c73dd9d5860f42e00765a7e34e8ca397a9
ms.openlocfilehash: 1a750bedee2aac667c84113d2d08daa20428c260


---

# 用于对管理权限进行划分的层模型

在当前的威胁环境中，如果攻击者获取了你的系统还不算是一个问题，那什么时候才是问题？ 实际上，内部安全与强大的外围防御同样重要。 本文介绍了一种安全模型，旨在通过从高风险区隔离高特权活动以防止特权提升。 该模型在提供一个良好的用户体验的同时仍坚持了最佳实践和安全原则。

## Active Directory 林中的特权提升

获得对 Windows Server Active Directory (AD) 林永久管理权限的用户、服务或应用程序帐户会为组织的任务和业务带来大量风险。 这些帐户通常是攻击者的目标，因为如果它们遭到破坏，那么攻击者将拥有连接到域中其他服务器或应用程序的权限。

层模型基于管理员所管理的资源在他们之间创建分区。 控制用户工作站的管理员与那些控制应用程序或管理企业标识的管理员相分离。 有关此模型的详细信息，请参阅 [Securing privileged access reference material](http://aka.ms/tiermodel)（保护特权访问的参考资料）。

## 通过登录限制来限制凭据公开

减少管理帐户的凭据被盗风险通常需要重新调整管理实践来限制向攻击者公开。 第一步，建议组织应当执行以下操作：

- 限制在其中公开管理凭据的主机数量。
- 将角色权限限制为最低要求。
- 确保管理任务不会在用于标准用户活动（例如，电子邮件和 Web 浏览）的主机上执行。

下一步是实现登录限制，并使过程和实践遵循层模型要求。 理想情况下，凭据公开还应减小为每个层中的角色所需的最小特权。

应强制执行登录限制，以确保高特权的帐户没有对安全级别较低的资源的访问权限。 例如：

- 域管理员（第 0 层）无法登录到企业服务器（第 1 层）和标准用户工作站（第 2 层）。
- 服务器管理员（第 1 层）无法登录到标准用户工作站（第 2 层）。

>[!NOTE]
> 服务器管理员不应在域管理员组中。 应为负责管理域控制器和企业服务器的人员提供独立的帐户。

可以通过以下方式强制执行登录限制：

- 组策略登录权限限制，包括：  
    - 拒绝从网络访问该计算机  
    - 拒绝作为批处理作业登录  
    - 拒绝作为服务登录  
    - 拒绝本地登录  
    - 拒绝通过远程桌面设置登录  
- 如果使用 Windows Server 2012 或更高版本，则使用身份验证策略和接收器
- 如果帐户在专用管理员林中，则使用选择性身份验证

下一篇文章[规划堡垒环境](planning-bastion-environment.md)将介绍如何添加 Microsoft Identity Manager 的专用管理林以建立管理帐户。



<!--HONumber=Jul16_HO3-->


