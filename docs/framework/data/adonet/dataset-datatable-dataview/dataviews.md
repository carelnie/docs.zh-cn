---
title: DataView
ms.date: 03/30/2017
ms.assetid: 0fe5dfa2-c1cd-435f-90b6-b4dd2e3ef34b
ms.openlocfilehash: f3e5d047496785c34c1fe242853829ae0110dc2a
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32758784"
---
# <a name="dataviews"></a>DataView
您可以利用 <xref:System.Data.DataView> 创建存储在 <xref:System.Data.DataTable>（一种通常在数据绑定应用程序中使用的功能）中的数据的不同视图。 使用**DataView**，您可以公开具有不同的排序顺序的表中的数据，并且你可以按行状态或基于筛选器表达式来筛选数据。  
  
 A **DataView**提供在基础数据的动态视图**DataTable**： 内容、 排序和成员身份反映的更改，在发生。 此行为不同于**选择**方法**DataTable**，它将返回<xref:System.Data.DataRow>表中的数组基于特定筛选器和/或排序顺序： thiscontent 反映对更改基础表，但其成员资格和顺序却保持不变。 动态功能**DataView**使其适合用于数据绑定应用程序。  
  
 A **DataView**你提供一组数据，类似于数据库视图，可向其应用不同排序和筛选条件的动态视图。 与数据库视图，但是，不同**DataView**不能作为表处理，并且无法提供联接的表的视图。 另外，还不能排除存在于源表中的列，也不能追加不存在于源表中的列（如计算列）。  
  
 你可以使用<xref:System.Data.DataView.DataViewManager%2A>来管理中的所有表的视图设置**数据集**。 **DataViewManager**提供了方便的方式来管理每个表的默认视图设置。 当一个控件绑定到多个表的**数据集**，绑定到**DataViewManager**是理想的选择。  
  
## <a name="in-this-section"></a>本节内容  
 [创建数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-a-dataview.md)  
 描述如何创建**DataView**为**DataTable**。  
  
 [对数据进行排序和筛选](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/sorting-and-filtering-data.md)  
 描述如何设置的属性**DataView**以返回满足指定筛选条件的数据行的子集，或以特定排序顺序返回数据。  
  
 [DataRow 和 DataRowView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datarows-and-datarowviews.md)  
 介绍如何访问由公开的数据**DataView**。  
  
 [查找行](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/finding-rows.md)  
 介绍如何以查找中的特定行**DataView**。  
  
 [ChildView 和关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/childviews-and-relations.md)  
 描述如何创建父-子关系中使用的数据的视图**DataView**。  
  
 [修改 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/modifying-dataviews.md)  
 描述如何修改在基础数据**DataTable**通过**DataView**，包括启用或禁用更新。  
  
 [处理 DataView 事件](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-dataview-events.md)  
 介绍如何使用**ListChanged**可以接收通知的事件时的内容或顺序**DataView**正在更新。  
  
 [管理 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/managing-dataviews.md)  
 介绍如何使用**DataViewManager**管理**DataView**每个表中的设置**数据集**。  
  
## <a name="related-sections"></a>相关章节  
 [ASP.NET Web 应用程序](http://msdn.microsoft.com/library/a812d7b7-049e-4234-a4c2-6acf690301f6)  
 提供创建 ASP.NET 应用程序、Web 窗体和 Web 服务的概述和详细步骤信息。  
  
 [Windows 应用程序](http://msdn.microsoft.com/library/a6bb2180-09b1-4738-b9fd-7fb05fc92f23)  
 提供有关使用 Windows 窗体和控制台应用程序的详细信息。  
  
 [数据集、数据表和数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 描述**数据集**对象以及如何使用它来管理应用程序数据。  
  
 [数据表](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)  
 描述**DataTable**对象以及如何使用它来管理应用程序数据本身或作为的一部分**数据集**。  
  
 [ADO.NET](../../../../../docs/framework/data/adonet/index.md)  
 描述 ADO.NET 结构和组件，并说明如何使用 ADO.NET 来访问现有的数据源和管理应用程序数据。  
  
## <a name="see-also"></a>请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)
