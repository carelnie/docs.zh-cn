---
title: 如何：在 XAML 中使用视图对数据进行排序和分组
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [WPF], grouping data in views in XAML
- XAML [WPF], sorting data in views
- grouping data in views in XAML [WPF]
- data binding [WPF], sorting data in views in XAML
- sorting data in views in XAML [WPF]
- XAML [WPF], grouping data in views
- views [WPF], sorting data
- views [WPF], grouping data
ms.assetid: 145c8c3f-dbdd-4d0d-816f-90b35eba7eda
ms.openlocfilehash: 80529420bcc5fdca473313e164b3d096732953f4
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33555823"
---
# <a name="how-to-sort-and-group-data-using-a-view-in-xaml"></a>如何：在 XAML 中使用视图对数据进行排序和分组
此示例演示如何创建数据集合中的视图[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。 视图允许分组、 排序、 筛选、 功能和当前项的概念。  
  
## <a name="example"></a>示例  
 在下面的示例中，静态资源名为*放置*指一套*位置*对象，其中的每个*位置*对象包含的城市名称和状态。 前缀*src*映射到命名空间中的数据源*位置*定义。 前缀*scm*映射到`"clr-namespace:System.ComponentModel;assembly=WindowsBase"`和*dat*映射到`"clr-namespace:System.Windows.Data;assembly=PresentationFramework"`。  
  
 下面的示例创建数据集合，它按状态分组并按城市名称排序的视图。  
  
 [!code-xaml[CollectionViewSource#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#1)]  
  
 视图随后可以绑定源，如以下示例所示：  
  
 [!code-xaml[CollectionViewSource#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#2)]  
  
 对于到 XML 数据中定义的绑定<xref:System.Windows.Data.XmlDataProvider>资源，XML 名称前面加上 @ 符号。  
  
 [!code-xaml[CollectionViewSource#XDPChunk](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#xdpchunk)]  
  
 [!code-xaml[CollectionViewSource#Attribute](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CollectionViewSource/CS/window1.xaml#attribute)]  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Windows.Data.CollectionViewSource>  
 [获取数据集合的默认视图](../../../../docs/framework/wpf/data/how-to-get-the-default-view-of-a-data-collection.md)  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)  
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)
