---
title: Windows Communication Foundation 示例的一次性安装过程
ms.date: 03/30/2017
ms.assetid: a5848ffd-3eb5-432d-812e-bd948ccb6bca
ms.openlocfilehash: 954ec04d2ef1ca7667b4f75a8a6652010b5dbd33
ms.sourcegitcommit: 43cbde34970f5f38f30c43cd63b9c7e2e83717ae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/11/2020
ms.locfileid: "81121619"
---
# <a name="one-time-setup-procedure-for-the-windows-communication-foundation-samples"></a>Windows Communication Foundation 示例的一次性安装过程

大多数 Windows 通信基础 （WCF） 示例托管在 Internet 信息服务 （IIS） 中，并且从公共虚拟目录运行。 此一次性设置过程在磁盘上创建一个文件夹;它还向名为 **"服务模型示例**"的 IIS 添加了一个虚拟目录。

**ServiceModelSample**虚拟目录用于生成和运行使用 IIS 托管服务的所有示例。 这是运行示例所需的唯一虚拟目录。 绑定示例将替换以前在此虚拟目录部署的所有服务；只有最近生成的示例将在此虚拟目录中部署并可用。

> [!NOTE]
> 必须在本地管理员帐户下运行所有命令。 如果使用 Windows 7、Windows Vista 或 Windows Server 2008 R2，则还必须使用提升的权限运行命令提示符。 为此，请右键单击命令提示图标，然后单击"**以管理员身份运行**"。 本主题中的所有命令都必须在具有合适路径设置的命令提示中运行。  确保这一点的最简单方法是使用 Visual Studio 命令提示。 要打开此提示，请单击 **"开始**"，选择 **"所有程序**"，向下滚动到**Visual Studio 2010**，选择**可视化工作室工具**，右键单击**视觉工作室命令提示（2010），** 然后单击"**以管理员身份运行**"。 如果安装了 Visual Studio 学习版，但此命令提示不可用，则必须向系统路径添加“C:\Windows\Microsoft.Net\Framework\v4.0”。

### <a name="one-time-setup-procedure-for-wcf-samples"></a>WCF 示例的一次性安装过程

1. 确保设置了ASP.NET。 有关如何设置ASP.NET的详细信息，请参阅[互联网信息服务托管说明](internet-information-service-hosting-instructions.md)。

2. 确保安装了 .NET 框架 4。 搜索以下目录搜索 v4.0（或更高版本）： **[Windows]Microsoft.NET_Framework**

3. 确保您安装了 Visual Studio 2012 或更高版本，或者您的操作系统是 Windows Server 2008 SP2 或更高版本。

4. 运行以下命令。 有关必须运行这些命令的原因的详细信息，请参阅[IIS 托管服务失败](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752252(v=vs.90))。

    > [!WARNING]
    > 如果重新安装 IIS，则需要再次运行以下命令。

    ```console
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\aspnet_regiis" –i –enable
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\ServiceModelReg.exe" -r
    ```

    > [!WARNING]
    > 运行该命令`aspnet_regiis –i –enable`将使默认应用池使用 .NET Framework 4 运行，这可能会为同一台计算机上的其他应用程序带来不兼容问题。

5. 按照[防火墙说明](firewall-instructions.md)启用示例使用的端口。

6. 检查以下默认目录：\<安装驱动器>：**\WF_WCF_Samples**。 如果之前已安装这些示例，则该目录为默认目录。

7. 如果未安装示例，请从 .NET 框架 4 的[Windows 通信基础 （WCF） 和 Windows 工作流基础 （WF） 示例](https://www.microsoft.com/download/details.aspx?id=21459)安装它们。

8. 安装示例后，转到 ：\<安装驱动器>：**{WF_WCF_Samples\WCF_\\安装程序**

9. 运行**Setupvroot.bat**批处理文件。 将执行以下步骤：

    - 将在 IIS 中创建一个名为 ServiceModelSamples 的虚拟目录。

    - 新建名为 %SystemDrive%\Inetpub\wwwroot\ServiceModelSamples 和 %SystemDrive%\Inetpub\wwwroot\ServiceModelSamples\bin 的磁盘目录。

    如果您希望手动设置这些目录，请参阅[虚拟目录设置说明](virtual-directory-setup-instructions.md)。 若要恢复此步骤中所进行的所有更改，请在使用完示例后运行一次 cleanupvroot.bat。

    > [!NOTE]
    > 除非运行 cleanupvroot.bat，否则此过程只能在计算机上执行一次。

10. 您必须向在其下生成示例的帐户和 Network Service 用户授予对 %SystemDrive%\inetpub\wwwroot 的修改权限。 在生成过程中，某些 Web 承载的示例可能会尝试将已编译的二进制文件复制到上述位置，如果你没有设置相应权限，则生成过程将中断。 或者，您可以保留权限，并将 SDK 命令提示符或 Visual Studio 命令提示符 （2012） 作为管理员运行，或者在 Visual Studio 2012 中生成示例，也可以作为管理员运行。

    > [!NOTE]
    > 如果未完成此步骤，IIS 承载的所有示例都将在生成时失败。 确保正确设置权限，或者同时以管理员身份运行 SDK 命令提示和 Visual Studio 命令提示 (2012)。

11. 在计算机上创建一个 C:\logs 目录；某些示例可能需要此目录。 确保向合适的帐户授予了对此文件夹的写访问权限。 对于 Windows 7、Windows Vista 和 Windows 服务器 2008 R2，此帐户为**网络服务**。 对于 Windows 服务器 2008，该帐户为 NT 颁发机构+网络服务。 对于 Windows XP 和 Windows 服务器 2003，该帐户为 ASPNET。

12. 运行 Setupcerttool.bat 文件。 此文件位于\<"安装路径>\WF_WCF_Samples_WCF_安装程序]文件夹中。  此脚本将执行以下任务：

    - 生成 FindPrivateKey 工具。

    - 创建一个名为 %ProgramFiles%\ServiceModelSampleTools 的目录。

    - 将新的 FindPrivateKey 工具复制到此目录。

    使用证书且承载于 IIS 中的示例需要使用此工具。

    > [!NOTE]
    > 出于安全方面的考虑，请记住在完成这些示例后，通过运行名为 Cleanupvroot.bat 的批处理文件来移除虚拟目录定义和在上面的设置步骤中授予的权限。

13. 自承载（不承载于 IIS 中）的示例需要在计算机上注册要侦听的 HTTP 地址的权限。 用于 HTTP 命名空间预留的权限由用于运行该示例的用户帐户提供。 默认情况下，管理员帐户具有注册任何 HTTP 地址的权限。 必须向非管理员帐户授予针对示例所使用的 HTTP 命名空间的权限。 有关如何配置命名空间预留的详细信息，请参阅[配置 HTTP 和 HTTPS](../feature-details/configuring-http-and-https.md)。

14. 有些示例需要使用消息队列。 有关安装说明，请参阅[安装消息队列 （MSMQ）。](installing-message-queuing-msmq.md)

    > [!NOTE]
    > 确保在运行需要消息队列的任何示例之前启动 MSMQ 服务。

15. 有些示例需要使用证书。 请参阅[互联网信息服务 （IIS） 服务器证书安装说明](iis-server-certificate-installation-instructions.md)。
