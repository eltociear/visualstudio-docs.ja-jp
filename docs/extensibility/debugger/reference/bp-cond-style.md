---
title: BP_COND_STYLE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_COND_STYLE
helpviewer_keywords:
- BP_COND_STYLE enumeration
ms.assetid: a93b1412-f447-48a1-af9d-38f3dbb3092f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ded3d31f9be2d0a02a238ead4bc989cc21b4922a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351824"
---
# <a name="bpcondstyle"></a>BP_COND_STYLE
保留中のブレークポイントの条件のスタイルを指定し、ブレークポイントをバインドします。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
typedef DWORD BP_COND_STYLE;
```

```csharp
public enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
```

## <a name="fields"></a>フィールド
`BP_COND_NONE`\
ブレークポイントの位置に達すると、ブレークポイントが発生します。 ブレークポイントの条件を指定します。

`BP_COND_WHEN_TRUE`\
評価される条件式がブレークポイントに関連付けられている場合のみ、ブレークポイントを発生させる`true`します。

`BP_COND_WHEN_CHANGED`\
条件付きの式の値は、ブレークポイントに関連付けられている場合にのみ、ブレークポイントがその以前の評価から変更が発生します。

## <a name="remarks"></a>Remarks
使用、`styleCondition`のメンバー、 [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)構造体。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
