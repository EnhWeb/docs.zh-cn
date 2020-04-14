---
title: 在 Azure HDInsight Spark 群集的 Jupyter Notebook 中安装 .NET for Apache Spark
description: 了解如何在 Azure HDInsight 的 Jupyter Notebook 中安装 .NET for Apache Spark。
ms.date: 03/13/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 32047efcde093a3752bdd59baa88896d1547b93e
ms.sourcegitcommit: 34dc3c0d0d0a1cc418abff259d9daa8078d00b81
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2020
ms.locfileid: "79546745"
---
# <a name="install-net-for-apache-spark-on-jupyter-notebooks-on-azure-hdinsight-spark-clusters"></a><span data-ttu-id="daef4-103">在 Azure HDInsight Spark 群集的 Jupyter Notebook 中安装 .NET for Apache Spark</span><span class="sxs-lookup"><span data-stu-id="daef4-103">Install .NET for Apache Spark on Jupyter notebooks on Azure HDInsight Spark clusters</span></span>

<span data-ttu-id="daef4-104">本文介绍如何在 Azure HDInsight Spark 群集的 Jupyter Notebook 中安装 .NET for Apache Spark。</span><span class="sxs-lookup"><span data-stu-id="daef4-104">This article teaches you how to install .NET for Apache Spark on Jupyter notebooks on Azure HDInsight Spark clusters.</span></span> <span data-ttu-id="daef4-105">可以通过搭配使用命令行和 Azure 门户在 Azure HDInsight 群集中部署 .NET for Apache Spark（有关详细信息，请参阅[如何将 .NET for Apache Spark 应用程序部署到 Azure HDInsight](../tutorials/hdinsight-deployment.md)），但笔记本可提供更好的交互和迭代体验。</span><span class="sxs-lookup"><span data-stu-id="daef4-105">You can deploy .NET for Apache Spark on Azure HDInsight clusters through a combination of the command line and the Azure portal (for more information, see [how to deploy a .NET for Apache Spark application to Azure HDInsight](../tutorials/hdinsight-deployment.md)), but notebooks provide a more interactive and iterative experience.</span></span>

<span data-ttu-id="daef4-106">Azure HDInsight 群集已附带 Jupyter Notebook，因此只需将 Jupyter Notebook 配置为运行 .NET for Apache Spark。</span><span class="sxs-lookup"><span data-stu-id="daef4-106">Azure HDInsight clusters already come with Jupyter notebooks, so all you have to do is configure the Jupyter notebooks to run .NET for Apache Spark.</span></span> <span data-ttu-id="daef4-107">若要在 Jupyter Notebook 中使用 .NET for Apache Spark，需要提供 C# REPL，以逐行执行 C# 代码并在必要时保留执行状态。</span><span class="sxs-lookup"><span data-stu-id="daef4-107">To use .NET for Apache Spark in your Jupyter notebooks, a C# REPL is needed to execute your C# code line-by-line and to preserve execution state when necessary.</span></span> <span data-ttu-id="daef4-108">[Try .NET](https://github.com/dotnet/try) 已集成为官方 .NET REPL。</span><span class="sxs-lookup"><span data-stu-id="daef4-108">[Try .NET](https://github.com/dotnet/try) has been integrated as the official .NET REPL.</span></span>

<span data-ttu-id="daef4-109">若要通过 Jupyter Notebook 体验启用 .NET for Apache Spark，需要通过 [Ambari](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-manage-ambari) 完成一些手动步骤，然后从 HDInsight Spark 群集提交[脚本操作](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)。</span><span class="sxs-lookup"><span data-stu-id="daef4-109">To enable .NET for Apache Spark through the Jupyter Notebooks experience, you need to follow a few manual steps through [Ambari](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-manage-ambari) and submit [script actions](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux) on the HDInsight Spark cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="daef4-110">此功能是试验功能，HDInsight Spark 团队不支持它。 </span><span class="sxs-lookup"><span data-stu-id="daef4-110">This feature is *experimental* and is not supported by the HDInsight Spark team.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daef4-111">先决条件</span><span class="sxs-lookup"><span data-stu-id="daef4-111">Prerequisites</span></span>

<span data-ttu-id="daef4-112">创建 [Azure HDInsight Spark](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-jupyter-spark-sql-use-portal#create-an-hdinsight-spark-cluster) 群集（如果还没有此群集）。</span><span class="sxs-lookup"><span data-stu-id="daef4-112">If you don't already have one, create an [Azure HDInsight Spark](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-jupyter-spark-sql-use-portal#create-an-hdinsight-spark-cluster) cluster.</span></span>

1. <span data-ttu-id="daef4-113">访问 [Azure 门户](https://portal.azure.com)并选择“+ 创建资源”。 </span><span class="sxs-lookup"><span data-stu-id="daef4-113">Visit the [Azure portal](https://portal.azure.com) and select **+ Create a Resource**.</span></span>

1. <span data-ttu-id="daef4-114">新建一个 Azure HDInsight 群集资源。</span><span class="sxs-lookup"><span data-stu-id="daef4-114">Create a new Azure HDInsight cluster resource.</span></span> <span data-ttu-id="daef4-115">在创建群集过程中，选择“Spark 2.4”和“HDI 4.0”。  </span><span class="sxs-lookup"><span data-stu-id="daef4-115">Select **Spark 2.4** and **HDI 4.0** during cluster creation.</span></span>

## <a name="install-net-for-apache-spark"></a><span data-ttu-id="daef4-116">安装 .NET for Apache Spark</span><span class="sxs-lookup"><span data-stu-id="daef4-116">Install .NET for Apache Spark</span></span>

<span data-ttu-id="daef4-117">在 Azure 门户中选择上一步中创建的 HDInsight Spark 群集。 </span><span class="sxs-lookup"><span data-stu-id="daef4-117">In the Azure portal, select the **HDInsight Spark cluster** you created in the previous step.</span></span>

### <a name="stop-the-livy-server"></a><span data-ttu-id="daef4-118">停止 Livy 服务器</span><span class="sxs-lookup"><span data-stu-id="daef4-118">Stop the Livy server</span></span>

1. <span data-ttu-id="daef4-119">从门户选择“概览”，然后选择“Ambari 主页”。  </span><span class="sxs-lookup"><span data-stu-id="daef4-119">From the portal, select **Overview**, and then select **Ambari home**.</span></span> <span data-ttu-id="daef4-120">出现提示时，请输入群集的登录凭据。</span><span class="sxs-lookup"><span data-stu-id="daef4-120">If prompted, enter the login credentials for the cluster.</span></span>

   ![停止 Livy 服务器](./media/hdinsight-notebook-installation/select-ambari.png)

2. <span data-ttu-id="daef4-122">从左侧导航菜单选择“Spark2”，然后选择“用于 Spark2 的 Livy 服务器”。  </span><span class="sxs-lookup"><span data-stu-id="daef4-122">Select **Spark2** from the left navigation menu, and select **LIVY FOR SPARK2 SERVER**.</span></span>

   ![停止 Livy 服务器](./media/hdinsight-notebook-installation/select-livyserver.png)

3. <span data-ttu-id="daef4-124">选择“hn0... host”。 </span><span class="sxs-lookup"><span data-stu-id="daef4-124">Select **hn0... host**.</span></span>

   ![停止 Livy 服务器](./media/hdinsight-notebook-installation/select-host.png)

4. <span data-ttu-id="daef4-126">选择“用于 Spark2 的 Livy 服务器”旁边的省略号，然后选择“停止”。  </span><span class="sxs-lookup"><span data-stu-id="daef4-126">Select the ellipsis next to **Livy for Spark2 Server** and select **Stop**.</span></span> <span data-ttu-id="daef4-127">出现提示时，选择“确定”以继续操作  。</span><span class="sxs-lookup"><span data-stu-id="daef4-127">When prompted, select **OK** to proceed.</span></span>

   <span data-ttu-id="daef4-128">停止用于 Spark2 的 Livy 服务器。</span><span class="sxs-lookup"><span data-stu-id="daef4-128">Stop Livy for Spark2 Server.</span></span>
   <span data-ttu-id="daef4-129">![停止 Livy 服务器](./media/hdinsight-notebook-installation/stop-server.png)</span><span class="sxs-lookup"><span data-stu-id="daef4-129">![Stop Livy Server](./media/hdinsight-notebook-installation/stop-server.png)</span></span>

5. <span data-ttu-id="daef4-130">对“hn1... host”重复前面的步骤  。</span><span class="sxs-lookup"><span data-stu-id="daef4-130">Repeat the previous steps for **hn1... host**.</span></span>

### <a name="submit-an-hdinsight-script-action"></a><span data-ttu-id="daef4-131">提交 HDInsight 脚本操作</span><span class="sxs-lookup"><span data-stu-id="daef4-131">Submit an HDInsight script action</span></span>

1. <span data-ttu-id="daef4-132">`install-interactive-notebook.sh` 是一个脚本，它可安装 .NET for Apache Spark 并可更改 Apache Livy 和 sparkmagic。</span><span class="sxs-lookup"><span data-stu-id="daef4-132">The `install-interactive-notebook.sh` is a script that installs .NET for Apache Spark and makes changes to Apache Livy and sparkmagic.</span></span> <span data-ttu-id="daef4-133">必须先创建并上传 `install-interactive-notebook.sh`，然后才可将脚本操作提交到 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="daef4-133">Before you submit a script action to HDInsight, you need to create and upload `install-interactive-notebook.sh`.</span></span>

   <span data-ttu-id="daef4-134">在本地计算机中新建名称为 install-interactive-notebook.sh 的文件，粘贴 [install-interactive-notebook.sh 内容](https://raw.githubusercontent.com/dotnet/spark/master/deployment/HDI-Spark/Notebooks/install-interactive-notebook.sh)中的内容。 </span><span class="sxs-lookup"><span data-stu-id="daef4-134">Create a new file named **install-interactive-notebook.sh** in your local computer and paste the contents of [install-interactive-notebook.sh contents](https://raw.githubusercontent.com/dotnet/spark/master/deployment/HDI-Spark/Notebooks/install-interactive-notebook.sh).</span></span>

   <span data-ttu-id="daef4-135">将此脚本上传到可从 HDInsight 群集访问的 [URI](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#understand-script-actions) 上。</span><span class="sxs-lookup"><span data-stu-id="daef4-135">Upload the script to a [URI](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#understand-script-actions) that's accessible from the HDInsight cluster.</span></span> <span data-ttu-id="daef4-136">例如 `https://<my storage account>.blob.core.windows.net/<my container>/<some dir>/install-interactive-notebook.sh`。</span><span class="sxs-lookup"><span data-stu-id="daef4-136">For example, `https://<my storage account>.blob.core.windows.net/<my container>/<some dir>/install-interactive-notebook.sh`.</span></span>

2. <span data-ttu-id="daef4-137">使用 [HDInsight 脚本操作](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)运行群集上的 `install-interactive-notebook.sh`。</span><span class="sxs-lookup"><span data-stu-id="daef4-137">Run `install-interactive-notebook.sh` on the cluster using [HDInsight Script Actions](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span></span>

   <span data-ttu-id="daef4-138">返回到 Azure 门户中的 HDI 群集，从左侧的选项中选择“脚本操作”。 </span><span class="sxs-lookup"><span data-stu-id="daef4-138">Return to your HDI cluster in the Azure portal, and select **Script actions** from the options on the left.</span></span> <span data-ttu-id="daef4-139">提交一个脚本操作，用于在 HDInsight Spark 群集上部署 .NET for Apache Spark REPL。</span><span class="sxs-lookup"><span data-stu-id="daef4-139">You submit one script action to deploy the .NET for Apache Spark REPL on your HDInsight Spark cluster.</span></span> <span data-ttu-id="daef4-140">使用以下设置：</span><span class="sxs-lookup"><span data-stu-id="daef4-140">Use the following settings:</span></span>

   |<span data-ttu-id="daef4-141">Property</span><span class="sxs-lookup"><span data-stu-id="daef4-141">Property</span></span>  |<span data-ttu-id="daef4-142">描述</span><span class="sxs-lookup"><span data-stu-id="daef4-142">Description</span></span>  |
   |---------|---------|
   | <span data-ttu-id="daef4-143">脚本类型</span><span class="sxs-lookup"><span data-stu-id="daef4-143">Script type</span></span> | <span data-ttu-id="daef4-144">自定义</span><span class="sxs-lookup"><span data-stu-id="daef4-144">Custom</span></span> |
   | <span data-ttu-id="daef4-145">“属性”</span><span class="sxs-lookup"><span data-stu-id="daef4-145">Name</span></span> | <span data-ttu-id="daef4-146">*安装 .NET for Apache Spark 交互式笔记本体验*</span><span class="sxs-lookup"><span data-stu-id="daef4-146">*Install .NET for Apache Spark Interactive Notebook Experience*</span></span> |
   | <span data-ttu-id="daef4-147">Bash 脚本 URI</span><span class="sxs-lookup"><span data-stu-id="daef4-147">Bash script URI</span></span> | <span data-ttu-id="daef4-148">向其上传 `install-interactive-notebook.sh` 的 URI。</span><span class="sxs-lookup"><span data-stu-id="daef4-148">The URI to which you uploaded `install-interactive-notebook.sh`.</span></span> |
   | <span data-ttu-id="daef4-149">节点类型</span><span class="sxs-lookup"><span data-stu-id="daef4-149">Node type(s)</span></span>| <span data-ttu-id="daef4-150">头节点和工作节点</span><span class="sxs-lookup"><span data-stu-id="daef4-150">Head and Worker</span></span> |
   | <span data-ttu-id="daef4-151">参数</span><span class="sxs-lookup"><span data-stu-id="daef4-151">Parameters</span></span> | <span data-ttu-id="daef4-152">.NET for Apache Spark 版本。</span><span class="sxs-lookup"><span data-stu-id="daef4-152">.NET for Apache Spark version.</span></span> <span data-ttu-id="daef4-153">可以查看 [.NET for Apache Spark 版本](https://github.com/dotnet/spark/releases)。</span><span class="sxs-lookup"><span data-stu-id="daef4-153">You can check [.NET for Apache Spark releases](https://github.com/dotnet/spark/releases).</span></span> <span data-ttu-id="daef4-154">例如，如果要安装 Sparkdotnet 版本 0.6.0，则为 `0.6.0`。</span><span class="sxs-lookup"><span data-stu-id="daef4-154">For example, if you want to install Sparkdotnet version 0.6.0 then it would be `0.6.0`.</span></span>

   <span data-ttu-id="daef4-155">当脚本操作状态旁边出现绿色勾选标记时，转到下一步。</span><span class="sxs-lookup"><span data-stu-id="daef4-155">Move to the next step when green checkmarks appear next to the status of the script action.</span></span>

### <a name="start-the-livy-server"></a><span data-ttu-id="daef4-156">启动 Livy 服务器</span><span class="sxs-lookup"><span data-stu-id="daef4-156">Start the Livy server</span></span>

<span data-ttu-id="daef4-157">按照[停止 Livy 服务器](#stop-the-livy-server)部分中的说明操作，来为主机 hn0 和 hn1 启动（而非停止）用于 Spark2 的 Livy 服务器。    </span><span class="sxs-lookup"><span data-stu-id="daef4-157">Follow the instructions in the [Stop Livy server](#stop-the-livy-server) section to **Start** (rather than **Stop**) the Livy for Spark2 Server for hosts **hn0** and **hn1**.</span></span>

### <a name="set-up-spark-default-configurations"></a><span data-ttu-id="daef4-158">设置 Spark 默认配置</span><span class="sxs-lookup"><span data-stu-id="daef4-158">Set up Spark default configurations</span></span>

1. <span data-ttu-id="daef4-159">从门户选择“概览”，然后选择“Ambari 主页”。  </span><span class="sxs-lookup"><span data-stu-id="daef4-159">From the portal, select **Overview**, and then select **Ambari home**.</span></span> <span data-ttu-id="daef4-160">出现提示时，请输入群集的群集登录凭据。</span><span class="sxs-lookup"><span data-stu-id="daef4-160">If prompted, enter the cluster login credentials for the cluster.</span></span>

2. <span data-ttu-id="daef4-161">依次选择“Spark2”和“配置”   。</span><span class="sxs-lookup"><span data-stu-id="daef4-161">Select **Spark2** and **CONFIGS**.</span></span> <span data-ttu-id="daef4-162">然后选择“自定义 spark2 默认值”  。</span><span class="sxs-lookup"><span data-stu-id="daef4-162">Then, select **Custom spark2-defaults**.</span></span>

   ![设置配置](./media/hdinsight-notebook-installation/spark-configs.png)

3. <span data-ttu-id="daef4-164">选择“添加属性...”，添加 Spark 默认设置。 </span><span class="sxs-lookup"><span data-stu-id="daef4-164">Select **Add Property...** to add Spark default settings.</span></span>

   ![添加属性](./media/hdinsight-notebook-installation/add-property.png)

   <span data-ttu-id="daef4-166">有三种独立的属性。</span><span class="sxs-lookup"><span data-stu-id="daef4-166">There are three individual properties.</span></span> <span data-ttu-id="daef4-167">在单一属性添加模式中使用文本属性类型一次添加一个属性。 </span><span class="sxs-lookup"><span data-stu-id="daef4-167">Add them one at a time using the **TEXT** property type in Single property add mode.</span></span> <span data-ttu-id="daef4-168">检查任何键/值前后是否没有任何多余的空格。</span><span class="sxs-lookup"><span data-stu-id="daef4-168">Check that you don't have any extra spaces before or after any of the keys/values.</span></span>

   * <span data-ttu-id="daef4-169">**属性 1**</span><span class="sxs-lookup"><span data-stu-id="daef4-169">**Property 1**</span></span>
       * <span data-ttu-id="daef4-170">键：&ensp;&ensp;`spark.dotnet.shell.command`</span><span class="sxs-lookup"><span data-stu-id="daef4-170">Key:&ensp;&ensp;`spark.dotnet.shell.command`</span></span>
       * <span data-ttu-id="daef4-171">值：`/usr/share/dotnet-tools/dotnet-try,kernel-server,--default-kernel,csharp`</span><span class="sxs-lookup"><span data-stu-id="daef4-171">Value: `/usr/share/dotnet-tools/dotnet-try,kernel-server,--default-kernel,csharp`</span></span>

   * <span data-ttu-id="daef4-172">**属性 2** 使用包含到前文中脚本操作的 .NET for Apache Spark 版本。</span><span class="sxs-lookup"><span data-stu-id="daef4-172">**Property 2** Use the version of .NET for Apache Spark which you had included in the previous script action.</span></span>
       * <span data-ttu-id="daef4-173">键：&ensp;&ensp;`spark.dotnet.packages`</span><span class="sxs-lookup"><span data-stu-id="daef4-173">Key:&ensp;&ensp;`spark.dotnet.packages`</span></span>
       * <span data-ttu-id="daef4-174">值：`["nuget: Microsoft.Spark, 0.6.0", "nuget: Microsoft.Spark.Extensions.Delta, 0.6.0"]`</span><span class="sxs-lookup"><span data-stu-id="daef4-174">Value: `["nuget: Microsoft.Spark, 0.6.0", "nuget: Microsoft.Spark.Extensions.Delta, 0.6.0"]`</span></span>

   * <span data-ttu-id="daef4-175">**属性 3**</span><span class="sxs-lookup"><span data-stu-id="daef4-175">**Property 3**</span></span>
       * <span data-ttu-id="daef4-176">键：&ensp;&ensp;`spark.dotnet.interpreter`</span><span class="sxs-lookup"><span data-stu-id="daef4-176">Key:&ensp;&ensp;`spark.dotnet.interpreter`</span></span>
       * <span data-ttu-id="daef4-177">值：`try`</span><span class="sxs-lookup"><span data-stu-id="daef4-177">Value: `try`</span></span>

   <span data-ttu-id="daef4-178">例如，下图捕获了用于添加属性 1 的设置：</span><span class="sxs-lookup"><span data-stu-id="daef4-178">For example, the following image captures the setting for adding property 1:</span></span>

   ![设置配置](./media/hdinsight-notebook-installation/add-sparkconfig.png)

   <span data-ttu-id="daef4-180">添加这三个属性后，选择“保存”。 </span><span class="sxs-lookup"><span data-stu-id="daef4-180">After adding the three properties, select **SAVE**.</span></span> <span data-ttu-id="daef4-181">若看到配置建议警告屏幕，选择“仍然继续”  。</span><span class="sxs-lookup"><span data-stu-id="daef4-181">If you see a warning screen of config recommendations, select **PROCEED ANYWAY**.</span></span>

4. <span data-ttu-id="daef4-182">重启受影响的组件。</span><span class="sxs-lookup"><span data-stu-id="daef4-182">Restart affected components.</span></span>

   <span data-ttu-id="daef4-183">添加新属性后，需要重启受更改影响的组件。</span><span class="sxs-lookup"><span data-stu-id="daef4-183">After adding the new properties, you need to restart components that were affected by the changes.</span></span> <span data-ttu-id="daef4-184">在顶部选择“重启”，然后从下拉列表选择“重启所有受影响的组件”。  </span><span class="sxs-lookup"><span data-stu-id="daef4-184">At the top, select **RESTART**, and then **Restart All Affected** from the drop-down.</span></span>

   ![设置配置](./media/hdinsight-notebook-installation/restart-affected.png)

   <span data-ttu-id="daef4-186">出现提示时，选择“确认全部重启”以继续，然后单击“确定”完成操作。  </span><span class="sxs-lookup"><span data-stu-id="daef4-186">When prompted, select **CONFIRM RESTART ALL** to continue, then click **OK** to finish.</span></span>

## <a name="submit-jobs-through-a-jupyter-notebook"></a><span data-ttu-id="daef4-187">通过 Jupyter Notebook 提交作业</span><span class="sxs-lookup"><span data-stu-id="daef4-187">Submit jobs through a Jupyter notebook</span></span>

<span data-ttu-id="daef4-188">完成前面的步骤后，现在可以通过 Jupyter Notebook 提交 .NET for Apache Spark 作业。</span><span class="sxs-lookup"><span data-stu-id="daef4-188">After finishing the previous steps, you can now submit your .NET for Apache Spark jobs through Jupyter notebooks.</span></span>

1. <span data-ttu-id="daef4-189">新建一个 .NET for Apache Spark 笔记本。</span><span class="sxs-lookup"><span data-stu-id="daef4-189">Create a new .NET for Apache Spark notebook.</span></span> <span data-ttu-id="daef4-190">从 Azure 门户的 HDI 群集启动 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="daef4-190">Launch a Jupyter notebook from your HDI cluster in the Azure portal.</span></span>

   ![启动 Jupyter Notebook](./media/hdinsight-notebook-installation/launch-notebook.png)

   <span data-ttu-id="daef4-192">然后选择“新建” > “.NET Spark (C#)”，创建一个笔记本。  </span><span class="sxs-lookup"><span data-stu-id="daef4-192">Then, select **New** > **.NET Spark (C#)** to create a notebook.</span></span>

   ![Jupyter 笔记本](./media/hdinsight-notebook-installation/create-sparkdotnet-notebook.png)

2. <span data-ttu-id="daef4-194">使用 .NET for Apache Spark 提交作业。</span><span class="sxs-lookup"><span data-stu-id="daef4-194">Submit jobs using .NET for Apache Spark.</span></span>

   <span data-ttu-id="daef4-195">使用以下代码片段创建 DataFrame：</span><span class="sxs-lookup"><span data-stu-id="daef4-195">Use the following code snippet to create a DataFrame:</span></span>

   ```csharp
   var df = spark.Range(0,5);
   df.Show();
   ```

   ![提交 Spark 作业](./media/hdinsight-notebook-installation/create-df.png)

   <span data-ttu-id="daef4-197">使用下面的代码片段注册用户定义的函数 (UDF)，并将此 UDF 与 DataFrame 一起使用：</span><span class="sxs-lookup"><span data-stu-id="daef4-197">Use the following code snippet to register a user-defined function (UDF) and use the UDF with DataFrames:</span></span>

   ```csharp
   var myawesomeudf = Udf<int, string>((id) => $"hello {id}");
   df.Select(myawesomeudf(df["id"])).Show();
   ```

   ![提交 Spark 作业](./media/hdinsight-notebook-installation/run-udf.png)

## <a name="next-steps"></a><span data-ttu-id="daef4-199">后续步骤</span><span class="sxs-lookup"><span data-stu-id="daef4-199">Next steps</span></span>

* [<span data-ttu-id="daef4-200">将 .NET for Apache Spark 应用程序部署到 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="daef4-200">Deploy a .NET for Apache Spark application to Azure HDInsight</span></span>](../tutorials/hdinsight-deployment.md)
* [<span data-ttu-id="daef4-201">HDInsight 文档</span><span class="sxs-lookup"><span data-stu-id="daef4-201">HDInsight Documentation</span></span>](https://docs.microsoft.com/azure/hdinsight/)