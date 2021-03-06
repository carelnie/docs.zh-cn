---
title: 默认值表（C# 参考）
description: 了解默认构造函数返回的值类型的默认值。
ms.date: 07/20/2015
helpviewer_keywords:
- constructors [C#], return values
- keywords [C#], new
- default constructor [C#]
- defaults [C#]
- value types [C#], initializing
- variables [C#], value types
- constructors [C#], default constructor
- types [C#], default constructor return values
ms.openlocfilehash: 634a55304534b4269487f29be1fbb4930f51d8ca
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33218785"
---
# <a name="default-values-table-c-reference"></a>默认值表（C# 参考）

下表显示默认构造函数返回的值类型的默认值。 默认构造函数使用 `new` 运算符进行调用，如下所示：

```csharp
int myInt = new int();
```

上一语句与如下语句效果相同：

```csharp
int myInt = 0;
```

请记住：不允许在 C# 中使用未初始化的变量。

|值类型|默认值|
|----------------|-------------------|
|[bool](bool.md)|`false`|
|[byte](byte.md)|0|
|[char](char.md)|'\0'|
|[decimal](decimal.md)|0M|
|[double](double.md)|0.0D|
|[enum](enum.md)|表达式 (E)0 生成的值，其中 E 是枚举标识符。|
|[float](float.md)|0.0F|
|[int](int.md)|0|
|[long](long.md)|0L|
|[sbyte](sbyte.md)|0|
|[short](short.md)|0|
|[struct](struct.md)|通过如下设置生成的值：将所有值类型的字段设置为其默认值，将所有引用类型的字段设置为 `null`。|
|[uint](uint.md)|0|
|[ulong](ulong.md)|0|
|[ushort](ushort.md)|0|

## <a name="see-also"></a>请参阅
 [C# 参考](../index.md)  
 [C# 编程指南](../../programming-guide/index.md)  
 [值类型表](value-types-table.md)  
 [值类型](value-types.md)  
 [内置类型表](built-in-types-table.md)  
 [类型参考表](reference-tables-for-types.md)
