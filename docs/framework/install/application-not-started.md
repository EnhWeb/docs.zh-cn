---
title: 排查“无法启动此应用程序”
description: 了解在出现“无法启动此应用程序”对话框时如何应对。
author: rpetrusha
ms.author: ronpet
ms.date: 09/05/2019
ms.openlocfilehash: 2534979e8dea886c2d7298c57e12b66d7a962c69
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401280"
---
# <a name="troubleshooting-a-this-application-could-not-be-started-error-message"></a>排查“无法启动此应用程序”错误消息

为 .NET Framework 开发的应用程序通常需要在系统上安装 .NET Framework 的特定版本。 在某些情况下，你可能会尝试运行应用程序，而不使用已安装的 .NET Framework 版本或所需版本。 这通常会产生如下错误对话框：

![无法启动此应用程序](media/application-not-started/app-could-not-be-started.png)

这通常表示存在以下情况之一：

- 系统上的 .NET Framework 安装已损坏。

- 无法检测到应用程序所需的 .NET Framework 版本。

若要解决此问题以便可以运行应用程序，请执行以下操作：

1. 下载 [.NET Framework Repair Tool (NetFxRepairTool.exe)](https://www.microsoft.com/download/details.aspx?id=30135)。 该工具会在下载完成后自动运行。

1. 如果 .NET Framework Repair Tool 建议执行任何其他操作，例如下图所示的操作，请选择“下一步”  。

   ![建议的更改](media/application-not-started/repair-tool-recommended-changes.png)

1. .NET Framework Repair Tool 会显示一个对话框，如下图所示，指出更改已完成。 当尝试重新运行应用程序时，请保持该对话框处于打开状态。 如果 .NET Framework Repair Tool 已识别并更正损坏的 .NET Framework 安装，则应该会成功运行。

   ![建议的更改](media/application-not-started/repair-tool-changes-complete.png)

1. 如果应用程序成功运行，请选择“完成”  按钮。 否则，请选择“下一步”  按钮。

1. 如果选择了“下一步”  按钮，则 .NET Framework Repair Tool 会显示如下所示的对话框。 选择“完成”  按钮，将诊断信息发送给 Microsoft。

   ![无法解决问题](media/application-not-started/repair-tool-no-resolution.png)

1. 如果仍无法运行应用程序，请安装 Windows 版本支持的最新版本 .NET Framework，如下表所示。

   |Windows 版本|.NET Framework 安装|
   |---|---|
   |Windows 10 周年更新及更高版本|[.NET Framework 4.8 Runtime](https://dotnet.microsoft.com/download/dotnet-framework/net48)|
   |Windows 10、Windows 10 11 月更新|[.NET Framework 4.6.2](https://www.microsoft.com/download/details.aspx?id=53345)|
   |Windows 8.1|[.NET Framework 4.8 Runtime](https://dotnet.microsoft.com/download/dotnet-framework/net48)|
   |Windows 8|[.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981)|
   |Windows 7 SP1|[.NET Framework 4.8 Runtime](https://dotnet.microsoft.com/download/dotnet-framework/net48)|
   |Windows Vista SP2|[.NET Framework 4.6](https://www.microsoft.com/download/details.aspx?id=48130)|

   > [!NOTE]
   >  .NET Framework 4.8 预安装在 Windows 10 2019 年 5 月更新上。

1. 尝试启动应用程序。

1. 在某些情况下，可能会显示一个对话框，要求你安装 .NET Framework 3.5。 选择“下载并安装此功能”  以安装 .NET Framework 3.5，然后重新启动应用程序。

   ![无法解决问题](media/application-not-started/install-3-5.png)

## <a name="see-also"></a>请参阅

- [.NET Framework 系统要求](../get-started/system-requirements.md)
- [.NET Framework 安装指南](index.md)
- [安装和卸载 .NET Framework 受阻疑难解答](troubleshoot-blocked-installations-and-uninstallations.md)