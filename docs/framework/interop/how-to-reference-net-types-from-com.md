---
title: 如何：从 COM 中引用 .NET 类型
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- importing type library
- COM interop, referencing .NET types
- interoperation with unmanaged code, referencing .NET types
- referencing .NET types
- interoperation with unmanaged code, importing type library
- type libraries
- COM interop, importing type library
ms.assetid: 54917f6f-cb18-4103-b622-856b55da93f3
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0333cd73240e685b46917d85afe0876532db3fd1
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33391893"
---
# <a name="how-to-reference-net-types-from-com"></a>如何：从 COM 中引用 .NET 类型
从客户端和服务器代码的角度看，COM 和 .NET Framework 之间的区别在很大程度上是不可见的。 Microsoft Visual Basic 客户端可在对象浏览器中查看 .NET 对象，这将公开对象方法和语法、属性和字段，正如任何其他 COM 对象那样。  
  
 尽管使用相同的工具将元数据导出到 COM 类型库，导入类型库的过程对于 C++ 客户端来说稍微复杂一些。 要从非托管 C++ 客户端引用 .NET 对象成员，通过“#import”指令引用 TLB 文件（使用 Tlbexp.exe 生成）。 从 C++ 引用类型库时，必须指定“raw_interfaces_only”选项或在基类库 Mscorlib.tlb 中导入定义。  
  
### <a name="to-import-a-library"></a>导入库  
  
-   在“#import”指令中指定“raw_interfaces_only”选项。 例如:  
  
    ```cpp  
    #import "..\LoanLib\LoanLib.tlb" raw_interfaces_only  
    ```  
  
     或  
  
-   包括用于 Mscorlib.tlb 的 #import 指令。 例如:  
  
    ```cpp  
    #import "mscorlib.tlb"  
    #import "..\LoanLib\LoanLib.tlb"  
    ```  
  
## <a name="see-also"></a>请参阅  
 [向 COM 公开 .NET Framework 组件](exposing-dotnet-components-to-com.md)  
 [向 COM 注册程序集](registering-assemblies-with-com.md)  
 [调用 .NET 对象](https://msdn.microsoft.com/library/40c9626c-aea6-4bad-b8f0-c1de462efd33(v=vs.100))  
 [为 COM 访问部署应用程序](https://msdn.microsoft.com/library/fb63564c-c1b9-4655-a094-a235625882ce(v=vs.100))
