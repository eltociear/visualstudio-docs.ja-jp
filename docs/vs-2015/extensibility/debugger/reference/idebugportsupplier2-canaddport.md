---
title: IDebugPortSupplier2::CanAddPort |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::CanAddPort
helpviewer_keywords:
- IDebugPortSupplier2::CanAddPort
ms.assetid: 41f69e0a-e82c-473d-8b7a-0c40fc5730fc
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e4ec078650446d3511ed9c5bdc8ee3ec0191487d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188355"
---
# <a name="idebugportsupplier2canaddport"></a>IDebugPortSupplier2::CanAddPort
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ポート サプライヤーが新しいポートを追加できることを確認します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT CanAddPort(   
   void   
);  
```  
  
```csharp  
int CanAddPort();  
```  
  
## <a name="return-value"></a>戻り値  
 ポートを追加できる場合を返します`S_OK`。 それ以外を返します`S_FALSE`を示すには、このポートのサプライヤーのポートは追加できません。  
  
## <a name="remarks"></a>Remarks  
 このメソッドを呼び出す前に、 [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)メソッド後者の方法は、ポートに追加するには、時間のかかる操作になることがありますを作成するためです。  
  
## <a name="see-also"></a>関連項目  
 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)   
 [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
