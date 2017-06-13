---
title: "服务跟踪查看器工具 (SvcTraceViewer.exe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 9027efd3-df8d-47ed-8bcd-f53d55ed803c
caps.latest.revision: 55
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 55
---
# 服务跟踪查看器工具 (SvcTraceViewer.exe)
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务跟踪查看器工具可帮助您分析 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 生成的诊断跟踪。服务跟踪查看器提供了一种方法，可以轻松地合并、查看和筛选日志中的跟踪消息，以便能够诊断、修复和验证 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务问题。  
  
## 配置跟踪  
 诊断跟踪提供的信息显示了应用程序操作过程中所发生的情况。顾名思义，您可以从操作来源跟踪操作直至目标，也可以通过中间点进行跟踪。  
  
 可以使用应用程序的配置文件（Web 承载的应用程序的 Web.config 或自承载应用程序的*Appname*.config）来配置跟踪。下面是一个示例：  
  
```  
<system.diagnostics>  
    <trace autoflush="true" />  
    <sources>  
            <source name="System.ServiceModel"   
                    switchValue="Information, ActivityTracing"  
                    propagateActivity="true">  
            <listeners>  
               <add name="sdt"   
                   type="System.Diagnostics.XmlWriterTraceListener"   
                   initializeData= "SdrConfigExample.e2e" />  
            </listeners>  
         </source>  
    </sources>  
</system.diagnostics>  
  
```  
  
 在此示例中，指定了跟踪侦听器的名称和类型。将侦听器命名为 `sdt` 并作为类型添加了标准 .NET Framework 跟踪侦听器 \(System.Diagnostics.XmlWriterTraceListener\)。`initializeData` 特性用于将该侦听器的日志文件的名称设置为 `SdrConfigExample.e2e`。对于该日志文件，还可以用一个简单文件名来替换完全限定路径。  
  
 此示例在名为 SdrConfigExample.e2e 的根目录中创建一个文件。当您使用跟踪查看器打开“打开和查看 WCF 跟踪文件”部分中所述的文件后，可以查看已发送的所有消息。  
  
 跟踪级别由 `switchValue` 设置控制。下表中描述了可用的跟踪级别。  
  
|跟踪级别|说明|  
|----------|--------|  
|严重|-   记录 Fail\-Fast 和事件日志项，并跟踪相关信息。下面是何时可使用“严重”级别的一些示例：<br />-   您的 AppDomain 由于未经处理的异常而失败。<br />-   您的应用程序未能启动。<br />-   导致故障的消息源自 MyApp.exe 进程。|  
|错误|-   记录所有异常。在下列情况下可以使用“错误”级别：<br />-   您的代码由于无效强制转换异常而崩溃。<br />-   “未能创建终结点”异常导致应用程序在启动时失败。|  
|警告|-   存在随后可能导致错误或严重故障的情况。在下列情况下可使用此级别：<br />-   应用程序正在接收的请求数比其限制设置所允许的数目要多。<br />-   接收队列占其配置容量的 98%。|  
|信息|-   生成对监视和诊断系统状态、测量性能或执行分析十分有用的消息。可以使用此类信息规划容量和管理性能。在下列情况下可使用此级别：<br />-   消息到达 AppDomain 并进行反序列化处理后出现错误。<br />-   创建 HTTP 绑定时出现错误。|  
|详细|-   同时针对用户代码和服务的调试级别跟踪。在下列情况下设置此级别：<br />-   您不确定在出现错误时调用了代码中的哪个方法。<br />-   您的某个终结点的配置出错并且无法启动服务，因为保留存储区中项被锁定。|  
|活动跟踪|处理活动与组件之间的流事件。<br /><br /> 此级别允许管理员和开发人员关联同一应用程序域中的各应用程序。<br /><br /> -   活动边界跟踪：启动\/停止。<br />-   传输跟踪。|  
  
 可以使用 `add` 指定要使用的跟踪侦听器的名称和类型。在示例配置中，将侦听器命名为 `sdt` 并作为类型添加了标准 .NET Framework 跟踪侦听器 \(`System.Diagnostics.XmlWriterTraceListener`\)。使用 `initializeData` 设置该侦听器的日志文件的名称。此外，还可以用一个简单文件名来替换完全限定路径。  
  
## 使用服务跟踪查看器工具  
  
### 打开并查看 WCF 跟踪文件  
 服务跟踪查看器支持三种文件类型：  
  
-   [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 跟踪文件 \(.svcLog\)  
  
-   事件跟踪文件 \(.etl\)  
  
-   Crimson 跟踪文件  
  
 通过服务跟踪查看器，可以打开任何受支持的跟踪文件、添加和集成附加跟踪文件，或同时打开和合并一组跟踪文件。  
  
##### 打开跟踪文件  
  
1.  通过使用命令窗口定位到 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 安装位置 \(C:\\Program Files\\Microsoft SDKs\\Windows\\v6.0\\Bin\)，然后键入 `SvcTraceViewer.exe`，可以启动服务跟踪查看器。  
  
> [!NOTE]
>  服务跟踪查看器工具可与两种文件类型关联：.svclog 和 .stvproj。在命令行中，可以使用两个参数来注册和注销文件扩展名。  
>   
>  \/register：将文件扩展名“.svclog”和“.stvproj”注册为与 SvcTraceViewer.exe 相关联  
>   
>  \/unregister：注销文件扩展名“.svclog”和“.stvproj”与 SvcTraceViewer.exe 的关联  
  
1.  当服务跟踪查看器启动时，单击**“文件”**，然后指向**“打开”**。定位到跟踪文件的存储位置。  
  
2.  双击要打开的跟踪文件。  
  
    > [!NOTE]
    >  按住 Shift 的同时单击多个跟踪文件，可以同时选中并打开这些文件。服务跟踪查看器合并所有文件的内容并显示为一个视图。例如，可以同时打开客户端和服务的跟踪文件。如果在配置中已启用消息日志记录和活动传播，则此功能十分有用。通过这种方式，可以检查客户端和服务之间的消息交换。还可以将多个文件拖动到查看器中，或使用**“项目”**选项卡。有关详细信息，请参见“管理项目”一节。  
  
3.  若要向打开的集合中添加更多跟踪文件，请单击**“文件”**，然后指向**“添加”**。在打开的窗口中，定位到跟踪文件的位置，然后双击要添加的文件。  
  
> [!CAUTION]
>  建议不要加载大于 200MB 的跟踪日志文件。如果尝试加载大于此限制的文件，加载过程可能要花很长时间，具体情况取决于计算机资源。服务跟踪查看器工具可能会长时间没有响应，或者该工具可能会耗尽计算机的内存。建议配置部分加载以避免这种情况。有关如何进行此配置的更多信息，请参见“加载大型跟踪文件”一节。  
  
#### 事件跟踪和 Crimson 跟踪  
 查看器的本机格式为 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 发出的活动跟踪格式。对于以其他格式发出的跟踪，必须先进行转换，这样查看器才会显示它们。目前，除了活动跟踪格式之外，查看器还支持事件跟踪和 crimson 跟踪。  
  
 打开不包含活动跟踪的文件时，查看器会尝试转换该文件。必须为将包含转换后的跟踪数据的文件指定名称和位置。数据转换完毕，查看器即会显示新文件的内容。  
  
> [!NOTE]
>  转换需要磁盘空间来存储转换后的跟踪数据。开始转换之前，请确保有足够的可用磁盘空间来存储数据。否则，转换将失败。  
  
### 管理项目  
 查看器支持项目，以便查看多个跟踪文件。例如，如果有客户端跟踪文件和服务跟踪文件，可以将它们添加到项目中。之后，每次打开该项目时，都会同时加载项目中的所有跟踪文件。  
  
 有两种管理项目的方法：  
  
-   在**“文件”**菜单中，可以打开、保存和关闭项目。  
  
-   在**“项目”**选项卡中，可以将文件添加到项目中。  
  
### 查看 WCF 跟踪  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 使用活动跟踪格式发出跟踪。在活动跟踪模型中，各个跟踪按其目的在活动中进行分组。逻辑控制流在活动之间传输。例如，在应用程序的生存期中，许多“消息发送活动”会出现和消失。有关查看跟踪和活动，以及服务跟踪查看器用户界面的更多信息，请参见[使用服务跟踪查看器查看相关跟踪和进行故障诊断](../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)。  
  
#### 切换到不同视图  
 服务跟踪查看器提供下列不同的视图。它们以选项卡的形式显示在查看器的左侧窗格，从**“视图”**菜单也可以访问这些视图。  
  
-   活动视图  
  
-   项目视图  
  
-   消息视图  
  
-   图形视图  
  
##### 活动视图  
 跟踪文件打开后，就可以查看分组到活动中并显示在左侧窗格**“活动”**视图中的跟踪。  
  
 **“活动”**视图显示活动名称、活动中的跟踪数、持续时间以及开始和结束时间。  
  
 单击所列出的任一活动，该活动中的跟踪都会显示在右侧跟踪窗格中。然后，选择一个跟踪即可查看其详细信息。  
  
 通过按**“Ctrl”**或**“Shift”**键并单击所需活动，可以选择多个活动。跟踪窗格显示所选活动的所有跟踪。  
  
 双击某个活动可以在**“图形”**视图中显示该活动。另一种方式是选择活动，然后切换到**“图形”**视图。  
  
> [!NOTE]
>  活动“000000000000”是一个特殊活动，不能在“图形”视图中显示。因为所有其他活动都与它链接，因此显示此活动会严重影响性能。  
  
 单击列标题可以对活动列表进行排序。包含警告跟踪的活动具有黄色背景，而包含错误跟踪的活动具有红色背景。  
  
 活动具有不同的类型，每种类型都与每个活动左侧的一个图标相对应。要了解其含义，可以参阅“了解跟踪图标”一节。  
  
##### 项目视图  
 在此视图中，可以管理当前项目中的跟踪文件。有关详细信息，请参见“管理项目”一节。  
  
##### 图形视图  
 服务跟踪查看器最强大的功能之一就是**“图形”**视图，它以图表形式显示给定活动的跟踪数据。通过图表形式，可以查看事件的逐步执行过程，可以查看当数据在多个活动之间移动时活动之间的相互关系。  
  
 若要切换到**“图形”**视图，请在**“活动”**视图中选择活动，然后单击**“活动”**选项卡，或者在**“消息”**视图中单击消息日志跟踪。如果加载了多个跟踪文件，并且活动涉及来自多个文件的跟踪，则所有相关的跟踪都会显示在“图形”视图中。双击活动和消息日志跟踪也可以切换到**“图形”**视图。  
  
 在**“图形”**视图中，每个垂直列都表示一个活动，列中的每个块都表示一个跟踪。活动按进程（或线程）分组。活动之间的小箭头表示传输。进程之间的大箭头表示消息交换。选定的活动始终为黄色。  
  
###### 在图形中选择跟踪  
  
1.  单击图形中的某个块。  
  
2.  使用向上键和向下键选择其相邻的跟踪。  
  
3.  查看“跟踪窗格”和“详细信息窗格”中的跟踪信息。  
  
###### 展开或折叠活动传输  
 当选定的活动传输到另一个活动时，可以展开活动传输。这样可以追踪这些传输。  
  
 若要展开或折叠活动传输，  
  
1.  定位到传输图标左侧带有“\+”号的传输跟踪。  
  
2.  单击“\+”号，或使用键盘按**“Ctrl”**和“\+”。  
  
3.  下一个活动出现在图形中。  
  
4.  在传输图标左侧会出现一个“\-”号。单击“\-”号或按 Ctrl 和“\-”，则会折叠活动传输。  
  
> [!NOTE]
>  当活动具有多个到它的传输时，如果展开其中一个传输，则会显示从根活动到新活动的活动。这些新活动以折叠形式显示。如果希望查看这些活动的详细信息，请在图形标题中单击展开图标将它们垂直展开。  
  
###### 垂直展开或折叠活动  
 查看器通过折叠活动在活动图形中隐藏不必要的详细信息。在折叠的活动中，不会显示各个跟踪。只会显示传输跟踪。如果想要查看活动中的所有跟踪，可通过单击图形标题中该活动的展开符号将活动垂直展开。  
  
 若要垂直展开或折叠活动，  
  
1.  单击活动标题中的“\+”图标可垂直展开活动。  
  
2.  请注意，所有跟踪都显示在图形中。  
  
3.  单击活动标题中的“\-”图标可垂直折叠活动。  
  
4.  请注意，活动中仅显示重要的传输、消息日志、警告和异常跟踪。  
  
###### 选项  
 在“图形”视图中可以从**“选项”**菜单中选择两个选项。  
  
-   显示活动边界跟踪：如果未选中此选项，则忽略图形中的活动边界跟踪。  
  
-   显示非消息详细跟踪：如果未选中此选项，则忽略除消息跟踪以外的其他详细级别跟踪。大多数情况下，详细级别的跟踪对于分析不是十分重要。如果不希望分析详细级别的跟踪，而只想关注更重要的跟踪，则此选项十分有用。  
  
###### 布局模式  
 查看器具有两种布局模式：**“进程”**和**“线程”**。此设置定义最大组织单位。默认的布局模式是**“进程”**，这种模式下，活动在图形中是按进程分组的。  
  
###### 执行列表  
 从该下拉列表中，可以选择要在图形中显示的进程或线程。例如，如果有两个客户端（A 和 B）的跟踪文件，并且打开了一个服务，而您只想在图形中显示该服务和客户端 A，则可以从列表中取消选择客户端 B。  
  
#### 查看跟踪详细信息  
 若要查看某个跟踪的详细信息，请在“跟踪”窗格中选择该跟踪。详细信息显示在“详细信息”窗格中。  
  
##### 跟踪窗格  
 服务跟踪查看器中的右上窗格为“跟踪”窗格。它列出了所选活动中的所有跟踪以及附加信息，例如跟踪级别、线程 ID 和进程名称。  
  
 通过右击跟踪，并选择**“将跟踪复制到剪贴板”**，可以将跟踪的原始 XML 复制到剪贴板。  
  
##### 详细信息窗格  
 服务跟踪查看器的右下窗格为“详细信息”窗格。它提供三个选项卡来查看跟踪的详细信息。  
  
 **“格式化”**视图以更为有序的方式显示信息。它以表和树的形式列出所有已知的 XML 元素，使得信息的读取和理解更加容易。  
  
 **“XML”**视图显示对应于所选跟踪的 XML。它支持突出显示和语法着色。当使用**“查找”**来搜索字符串时，它会突出显示搜索结果。  
  
 **“消息”**视图显示消息日志跟踪中 XML 的消息部分。选择非消息跟踪时，该视图不可见。  
  
### 筛选 WCF 跟踪  
 若要使跟踪的分析更加容易，可以通过以下方式对其进行筛选：  
  
-   筛选器工具栏提供对预定义筛选器和自定义筛选器的访问。可以通过**“视图”**菜单启用该工具栏。  
  
-   查看器的预定义筛选器可用来有选择地对部分 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 跟踪进行筛选。默认情况下，此筛选器设置为允许所有基础结构跟踪通过。此筛选器的设置在**“视图”**菜单之下的**“筛选器选项”**子菜单中定义。  
  
-   自定义 XPath 筛选器赋予用户对筛选的完全控制权。可以在**“视图”**菜单下**“自定义筛选器”**中对这些筛选器进行定义。  
  
 仅显示通过所有筛选器的跟踪。  
  
#### 使用筛选器工具栏  
 筛选器工具栏显示在工具的顶部。如果它未显示，可以在**“视图”**菜单中将其激活。此工具栏具有三个组件：  
  
-   查找：**“查找”**定义在筛选操作中要查找的主题。例如，如果要查找在进程 X 的上下文中发出的所有跟踪，请将该字段设置为 X，并将**“搜索范围”**字段设置为“进程名称”。如果选择了某个基于时间的筛选器，则此字段更改为 DateTime 选择器控件。  
  
-   搜索范围：此字段定义要应用的筛选器类型。  
  
-   级别：级别设置定义筛选器允许的最小跟踪级别。例如，如果级别设置为“错误及严重错误”，则只会显示“错误”和“严重”级别的跟踪。此筛选器与“查找”和“搜索范围”指定的条件结合使用。  
  
 **“立即筛选”**按钮将启动筛选操作。某些筛选器，尤其是当它们应用于大型数据集时，需要很长时间才能完成操作。可以通过按**“操作”**菜单下状态栏中显示的**“停止”**按钮来取消筛选操作。  
  
 **“清除”**按钮可重置预定义和自定义的筛选器，从而允许所有跟踪通过。  
  
#### 筛选器选项  
 查看器可以自动从视图中移除 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 跟踪。它可以有选择地移除由 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 的特定区域发出的跟踪，例如，从视图中移除与事务相关的跟踪。  
  
 此筛选器的设置在**“视图”**菜单之下的**“筛选器选项”**子菜单中定义。  
  
#### 自定义筛选器  
 如果熟悉 XML 路径语言 \(XPath\)，则可以使用它来构造自定义筛选器，以便搜索任何相关的 XML 元素的跟踪数据。可以通过筛选器工具栏访问这些筛选器。  
  
 自定义筛选器可以包括参数。此外，还可以导入预先存在的自定义筛选器。  
  
##### 创建自定义筛选器  
 可以通过两种方式创建筛选器：  
  
###### 使用模板向导创建自定义筛选器  
 可以单击现有跟踪并基于此跟踪的结构来创建筛选器。此示例创建基于线程 ID 的自定义筛选器。  
  
1.  在查看器右上区域的跟踪窗格中，选择包含待筛选元素的跟踪。  
  
2.  单击位于跟踪窗格顶部的**“创建自定义筛选器”**按钮。  
  
3.  在出现的对话框中，输入筛选器名称。在此示例中，输入 `Thread ID`。此外，还可以提供筛选器说明。  
  
4.  左侧的树视图显示您在步骤 1 中选择的跟踪记录的结构。通过浏览找到要为其创建条件的元素。在此示例中，浏览到位于 XPath: \/E2ETraceEvent\/System\/Execution\/@ThreadID 节点的 ThreadID。在树视图中双击“ThreadID”属性。这样可在对话框右侧为该属性创建一个表达式。  
  
5.  将 ThreadID 条件的参数字段从“无”更改为“{0}”。通过这一步骤，在应用筛选器时就可以配置 ThreadID 值。（请参见“如何应用筛选器”一节）最多可以定义四个参数。条件是用“或”运算符组合在一起的。  
  
6.  单击**“确定”**创建筛选器。  
  
> [!NOTE]
>  使用模板向导创建筛选器后，只能手动对其进行编辑。对于以前创建的筛选器，将无法激活向导。此外，在模板向导中创建的 XPath 筛选器的条件是用“或”运算符组合在一起的。如果需要“与”运算，可以在筛选器创建之后编辑筛选器表达式。  
  
###### 手动创建自定义筛选器  
 利用“自定义筛选器”菜单可以手动输入 XPath 筛选器。  
  
1.  在“视图”菜单上，单击**“自定义筛选器”**菜单项。  
  
2.  在出现的对话框中单击**“新建”**。  
  
3.  至少应指定筛选器名称和 XPath 表达式。  
  
4.  单击**“确定”**。  
  
###### 应用自定义筛选器  
 创建了自定义筛选器后，可以通过筛选器工具栏来访问它。在筛选器工具栏的**“搜索范围”**字段中选择要应用的筛选器。对上一示例，选择“Thread ID”。  
  
1.  在**“查找内容”**字段中指定要查找的值。在此示例中，输入要搜索的线程 ID。  
  
2.  单击**“立即筛选”**，然后观察操作结果。  
  
 如果筛选器使用多个参数，请使用“;”作为分隔符，在**“查找内容”**字段中输入这些参数。例如，以下字符串定义 3 个参数：“1;findValue;text”。查看器将“1”应用到筛选器的 {0} 参数。“findValue”和“text”分别应用到 {1} 和 {2}。  
  
###### 共享自定义筛选器  
 可以在不同会话和不同用户之间共享自定义筛选器。可以将筛选器导出到一个定义文件，然后在另一个位置导入该文件。  
  
 导入自定义筛选器：  
  
1.  在**“视图”**菜单上单击**“自定义筛选器”**。  
  
2.  在打开的对话框中单击**“导入”**按钮。  
  
3.  定位到自定义筛选器文件 \(.stvcf\)，单击该文件，然后单击**“打开”**按钮。  
  
 导出自定义筛选器：  
  
1.  在“视图”菜单上单击**“自定义筛选器”**。  
  
2.  在打开的对话框中选择要导出的筛选器。  
  
3.  单击**“导出”**按钮。  
  
4.  指定自定义筛选器定义文件 \(.stvcf\) 的名称和位置，然后单击**“保存”**按钮。  
  
> [!NOTE]
>  这些自定义筛选器只能从服务跟踪查看器导入和导出。其他工具无法读取这些筛选器。  
  
### 查找数据  
 查看器提供了以下方式来查找数据：  
  
-   通过“查找”工具栏，可以快速访问最常用的查找选项。  
  
-   “查找”对话框提供了更多查找选项。通过**“编辑”**菜单或快捷键 Ctrl \+ F，可以访问该对话框。  
  
 “查找”工具栏显示在查看器的顶部。如果它未显示，可以在**“视图”**菜单中将其激活。此工具栏具有两个组件：  
  
-   查找内容：可在其中输入搜索关键字。  
  
-   查找范围：可在其中输入搜索范围。可以选择在所有活动中搜索，也可以选择仅在当前活动中搜索。  
  
 查找对话框提供两个附加选项：  
  
-   查找目标：  
  
    -   如果选择“原始日志数据”选项，则会在所有原始数据中搜索关键字。  
  
    -   如果选择“XML 文本”和“XML 属性”选项，则仅在 XML 元素中搜索。  
  
    -   如果选择“已记录消息”选项，则仅在消息中搜索关键字。  
  
-   忽略根活动：搜索会忽略“000000000000”活动中的跟踪。如果根活动有数千个跟踪，而其中大多数为传输跟踪时，选择此选项会提高大型跟踪文件的性能。  
  
### 定位跟踪  
 由于在应用程序运行时期间，跟踪是逐步记录的，因此定位跟踪有助于调试应用程序。服务跟踪查看器提供多种定位跟踪方法。  
  
#### 逐步向前或逐步向后  
 如果将每个跟踪都看作程序中的一行代码，则逐步向前非常类似于 Visual Studio 集成开发环境 \(IDE\) 中的“逐过程”。区别在于，在跟踪中还可以逐步向后。逐步向前意味着移动到活动中的下一个跟踪。  
  
-   逐步向前：使用**“活动”**菜单，或者按“F10”。此外，还可以在跟踪窗格中使用“向下”箭头键。  
  
-   逐步向后：使用**“活动”**菜单，或者按“F9”。此外，还可以在跟踪窗格中使用“向上”箭头键。  
  
> [!NOTE]
>  此操作可能会跳转到其他进程中或者甚至其他计算机上发生的活动，因为 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 消息可以传送跨计算机的活动 ID。  
  
#### 追踪传输  
 传输跟踪是跟踪文件中的特殊跟踪。一个活动可以通过传输跟踪而传输到另一个活动。例如，“活动 A”可以传输到“活动 B”。在这种情况下，在“活动 A”中存在一个名为“至：活动”并带有传输图标的传输跟踪。此传输跟踪是两个跟踪之间的链接。在“活动 B”中，也可能存在一个传输跟踪，在活动结束时传输回“活动 A”。这类似于程序中的函数调用：A 调用 B，然后 B 返回。  
  
 “追踪传输”类似于调试器中的“单步执行”。它追踪从 A 到 B 的传输。它对其他跟踪没有任何影响。  
  
 有两种追踪传输的方法：使用鼠标或使用键盘：  
  
-   使用鼠标：在跟踪窗格中双击传输跟踪。  
  
-   使用键盘：选择传输跟踪，然后使用**“活动”**菜单中的“追踪传输”，或者按“F11”  
  
> [!NOTE]
>  在很多情况下，当活动 A 传输到活动 B 时，活动 A 会等待，直到活动 B 传输回活动 A 为止。这意味着活动 A 在活动 B 主动跟踪期间没有记录跟踪。但是，也有可能活动 A 不等待，而是持续记录跟踪。此外，活动 B 还可能不传输回活动 A。因此在这个意义上，活动传输与函数调用仍有不同。在图形视图中可以更好地理解活动传输。  
  
#### 跳转到下一个或上一个传输  
 在分析当前活动或选定的活动（如果选择了多个活动）时，可能希望快速找到它传输到的活动。通过“跳转到下一个传输”，可以定位到活动中的下一个传输跟踪。一旦找到传输跟踪，就可以使用“追踪传输”来单步执行下一个活动。  
  
-   跳转到下一个传输：使用**“活动”**菜单；或者按“Ctrl \+ F10”。  
  
-   跳转到上一个传输：使用**“活动”**菜单；或者按“Ctrl \+ F9”。  
  
#### 在图形视图中定位  
 尽管在活动窗格和跟踪窗格中定位类似于调试，使用**“图形”**视图还是能提供更好的定位体验。有关更多信息，请参见“图形视图”一节。  
  
### 加载大型跟踪文件  
 跟踪文件可能非常大。例如，如果启用“详细”级别跟踪，在运行几分钟后，结果跟踪文件很容易就可以达到数百兆字节，甚至更大，具体取决于网络速度和通信模式。  
  
 在服务跟踪查看器中打开极大型的跟踪文件时，系统性能可能会受到负面影响。加载速度和加载后的响应时间可能会很慢。实际速度不总是相同，具体取决于硬件配置。在大多数 PC 中，如果加载大于 200M 的跟踪文件，则会严重影响性能。对于大于 1G 的跟踪文件，此工具可能会用尽所有可用的内存，或者长时间停止响应。  
  
 为避免在分析大型跟踪文件时加载和响应时间变慢，服务跟踪查看器提供了一种称为“部分加载”的功能，即一次仅加载跟踪的一小部分。例如，您可能有一个大于 1GB 的跟踪文件，在服务器上已运行了几天。当发生某些错误，又想分析该跟踪时，将不必打开整个跟踪文件。您可以加载可能发生错误的某个时间段内的跟踪。由于缩小了范围，服务跟踪查看器工具可以更快地加载文件，而您可以使用一个较小的数据集来标识这些错误。  
  
#### 启用部分加载  
 部分加载不需要手动启用。如果试图加载的跟踪文件的总大小超过 40MB，服务跟踪查看器会自动显示“部分加载”对话框，供您选择要加载的部分。  
  
> [!NOTE]
>  由于跟踪在时间跨度内不一定均匀分布，因此，在“部分加载”工具栏中指定的时间段长度也不一定与显示的加载大小成正比。实际加载大小可以小于部分加载对话框中的“估计大小”。  
  
#### 调整部分加载  
 部分加载跟踪文件之后，可能希望更改已加载的数据集。通过调整查看器顶部的“部分加载”工具栏，可以实现此操作。  
  
1.  使用鼠标移动工具栏，或输入“开始时间”和“结束时间”。  
  
2.  单击**“调整”**按钮。  
  
## 了解跟踪图标  
 下面列出了服务跟踪查看器工具用于在**“活动”**视图、**“图形”**视图和**“跟踪”**窗格中表示不同项的图标。  
  
> [!NOTE]
>  某些未分类的跟踪（例如，“已关闭消息”）没有图标。  
  
### 活动跟踪  
  
|图标|说明|  
|--------|--------|  
|![警告跟踪](../../../docs/framework/wcf/media/7457c4ed-8383-4ac7-bada-bcb27409da58.gif "7457c4ed\-8383\-4ac7\-bada\-bcb27409da58")|“警告”跟踪：在警告级别发出的跟踪|  
|![错误跟踪](../../../docs/framework/wcf/media/7d908807-4967-4f6d-9226-d52125db69ca.gif "7d908807\-4967\-4f6d\-9226\-d52125db69ca")|“错误”跟踪：在错误级别发出的跟踪。|  
|![活动开始跟踪：](../../../docs/framework/wcf/media/8a728f91-5f80-4a95-afe8-0b6acd6e0317.gif "8a728f91\-5f80\-4a95\-afe8\-0b6acd6e0317")|“活动开端”跟踪：标记活动开头的跟踪。它包含活动的名称。应用程序设计人员或开发人员应为每个进程或线程的每个活动 ID 定义一个活动“开端”跟踪。<br /><br /> 如果活动 ID 在跟踪关联的跟踪源之间传播，随后将可看到同一活动 ID 有多个“开端”（每个跟踪源一个）。如果为跟踪源启用了 ActivityTracing，则会发出“开端”跟踪。|  
|![活动停止跟踪](../../../docs/framework/wcf/media/a0493e95-653e-4af8-84a4-4d09a400bc31.gif "a0493e95\-653e\-4af8\-84a4\-4d09a400bc31")|“活动结尾”跟踪：标记活动结尾的跟踪。.它包含活动的名称。应用程序设计人员或开发人员应为每个跟踪源的每个活动 ID 定义一个活动“结尾”跟踪。在给定跟踪源发出的活动结尾之后不会显示该跟踪源中的任何跟踪，除非跟踪时间间隔不够小。如果发生这种情况，时间相同的两个跟踪（包括“结尾”跟踪）在显示时可能会交错。如果活动 ID 在跟踪关联的跟踪源之间传播，将可看到同一活动 ID 有多个“结尾”（每个跟踪源一个）。如果为跟踪源启用了 ActivityTracing，则会发出“结尾”跟踪。|  
|![活动挂起跟踪](../../../docs/framework/wcf/media/6f7f4191-df2b-4592-8998-8379769e2d32.gif "6f7f4191\-df2b\-4592\-8998\-8379769e2d32")|“活动挂起”跟踪：标记活动暂停时间的跟踪。在活动继续之前，不会在挂起的活动中发出任何跟踪。挂起的活动表示不会在该活动的跟踪源范围内进行任何处理。“挂起”\/“继续”跟踪对于进行分析十分有用。如果为跟踪源启用了 ActivityTracing，则会发出“挂起”跟踪。|  
|![活动继续跟踪](../../../docs/framework/wcf/media/1060d9d2-c9c8-4e0a-9988-cdc2f7030f17.gif "1060d9d2\-c9c8\-4e0a\-9988\-cdc2f7030f17")|“活动继续”跟踪：标记活动在暂停后继续进行的时间的跟踪。可以在该活动中再次发出跟踪。“挂起”\/“继续”跟踪对于进行分析十分有用。如果为跟踪源启用了 ActivityTracing，则会发出“继续”跟踪。|  
|![传输](../../../docs/framework/wcf/media/b2d9850e-f362-4ae5-bb8d-9f6f3ca036a5.gif "b2d9850e\-f362\-4ae5\-bb8d\-9f6f3ca036a5")|传输：将逻辑控制流从一个活动传输到另一个活动时发出的跟踪。作为传输来源的活动可以继续与作为传输目标的活动并行工作。如果为跟踪源启用了 ActivityTracing，则会发出“传输”跟踪。|  
|![传输来源](../../../docs/framework/wcf/media/1df215cb-b344-4f36-a20d-195999bda741.gif "1df215cb\-b344\-4f36\-a20d\-195999bda741")|传输自：定义从另一个活动到当前活动的传输的跟踪。|  
|![传输目标](../../../docs/framework/wcf/media/74255b6e-7c47-46ef-8e53-870c76b04c3f.gif "74255b6e\-7c47\-46ef\-8e53\-870c76b04c3f")|传输至：定义从当前活动到另一个活动的逻辑控制流传输的跟踪。|  
  
### WCF 跟踪  
  
|图标|说明|  
|--------|--------|  
|![消息日志跟踪](../../../docs/framework/wcf/media/7c66e994-2476-4260-a0db-98948b9af197.gif "7c66e994\-2476\-4260\-a0db\-98948b9af197")|“消息日志”跟踪：在消息日志记录功能记录 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 消息时发出的跟踪（如果启用了 `System.ServiceModel.MessageLogging` 跟踪源）。单击此跟踪可以显示消息。一条消息有四个可配置的日志记录点：ServiceLevelSendRequest、TransportSend、TransportReceive 和 ServiceLevelReceiveRequest，消息日志跟踪的 `messageSource` 属性中也指明了它们。|  
|![“接收的消息”跟踪](../../../docs/framework/wcf/media/de4f586c-c5dd-41ec-b1c3-ac56b4dfa35c.gif "de4f586c\-c5dd\-41ec\-b1c3\-ac56b4dfa35c")|“已接收消息”跟踪：收到 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 消息时发出的跟踪（如果在“信息”或“详细”级别启用了 `System.ServiceModel` 跟踪源）。此跟踪对于在活动**“图形”**视图中查看消息相关箭头而言是必需的。|  
|![“已发送的消息”跟踪](../../../docs/framework/wcf/media/558943c4-17cf-4c12-9405-677e995ac387.gif "558943c4\-17cf\-4c12\-9405\-677e995ac387")|“已发送消息”跟踪：发送 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 消息时发出的跟踪（如果在“信息”或“详细”级别启用了 `System.ServiceModel` 跟踪源）。此跟踪对于在活动**“图形”**视图中查看消息相关箭头而言是必需的。|  
  
### 活动  
  
|图标|说明|  
|--------|--------|  
|![Activity](../../../docs/framework/wcf/media/wcfc-defaultactivityc.gif "wcfc\_defaultActivityc")|活动：指示当前活动为一般活动。|  
|![根活动](../../../docs/framework/wcf/media/5dc8e0eb-1c32-4076-8c66-594935beaee9.gif "5dc8e0eb\-1c32\-4076\-8c66\-594935beaee9")|根活动：指示进程的根活动。|  
  
### WCF 活动  
  
|图标|说明|  
|--------|--------|  
|![环境活动](../../../docs/framework/wcf/media/29fa00ac-cf78-46e5-822d-56222fff61d1.gif "29fa00ac\-cf78\-46e5\-822d\-56222fff61d1")|“环境”活动：可创建、打开或关闭 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 宿主或客户端的活动。在这些阶段中发生的错误将出现在此活动中。|  
|![Listen 活动](../../../docs/framework/wcf/media/d7b135f6-ec7d-45d7-9913-037ab30e4c26.gif "d7b135f6\-ec7d\-45d7\-9913\-037ab30e4c26")|“侦听”活动：可对与侦听器相关的跟踪进行记录的活动。可以在此活动内查看侦听器信息和连接请求。|  
|![接收字节活动](../../../docs/framework/wcf/media/2f628580-b80f-45a7-925b-616c96426c0e.gif "2f628580\-b80f\-45a7\-925b\-616c96426c0e")|“接收字节”活动：一种活动，可对与在两个终结点之间的连接上接收传入字节相关的所有跟踪进行分组。在与传播其活动 ID 的传输活动（比如 http.sys）建立关联时，此活动是必需的。诸如中止等连接错误将出现在此活动中。|  
|![过程消息活动](../../../docs/framework/wcf/media/wcfc-executionactivityiconc.GIF "wcfc\_ExecutionActivityIconc")|“处理消息”活动：一种活动，可对与创建 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 消息相关的跟踪进行分组。由于包装错误或消息格式不正确而导致的错误将出现在该活动中。可以在此活动内检测消息头，以确定是否从调用方传播了活动 ID。如果已传播，则在传输到“处理操作”活动（下一个图标）时，我们还可以为该活动分配传播的活动 ID，以便在调用方和被调用方的跟踪之间建立关联。|  
|![消息日志跟踪](../../../docs/framework/wcf/media/7c66e994-2476-4260-a0db-98948b9af197.gif "7c66e994\-2476\-4260\-a0db\-98948b9af197")|“处理操作”活动：一种活动，可对与两个终结点之间的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 请求相关的所有跟踪进行分组。如果配置中两个终结点上的 `propagateActivity` 都设置为 `true`，则会将来自两个终结点的所有跟踪合并为一个活动，以便直接关联。此类活动将包含由于传输或安全处理、延伸到用户代码边界及回退（如果存在响应）而发生的错误。|  
|![过程消息活动](../../../docs/framework/wcf/media/wcfc-executionactivityiconc.GIF "wcfc\_ExecutionActivityIconc")|“执行用户代码”活动：一种可对用户代码跟踪进行分组以处理请求的活动。|  
  
## 疑难解答  
 如果没有写入注册表的权限，在使用“`svctraceviewer /register`”命令注册工具时，将收到以下错误消息：“未在系统中注册 Microsoft 服务跟踪查看器”。如果出现这种情况，您应使用对注册表有写访问权限的帐户登录。  
  
 此外，服务跟踪查看器工具会将一些设置（例如，自定义筛选器和筛选器选项）写入其程序集文件夹中的 SvcTraceViewer.exe.settings 文件。如果没有该文件的读权限，您仍然能够启动工具，但无法加载设置。  
  
 如果在打开 .etl 文件时收到错误消息“处理一个或多个跟踪时出现未知错误”，则意味着 .etl 文件的格式无效。  
  
 如果打开使用阿拉伯语操作系统创建的跟踪日志，您可能会注意到时间筛选器不起作用。例如，2005 年对应于阿拉伯日历中的 1427 年。但是，服务跟踪查看器工具筛选器所支持的时间范围不支持早于 1752 年的日期。这表示您不能在筛选器中选择正确的日期。为了解决此问题，您可以使用 XPath 表达式创建一个自定义筛选器（**“视图”\/“自定义筛选器”**），以便包括特定的时间范围。  
  
## 请参阅  
 [使用服务跟踪查看器查看相关跟踪和进行故障诊断](../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)   
 [配置跟踪](../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)   
 [Activity Tracing and Propagation for End\-To\-End Trace Correlation](http://msdn.microsoft.com/zh-cn/2c11a905-64f8-47b5-bae5-a74fc666137e)