---
title: IDebugProcess3::Execute |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProcess3::Execute
helpviewer_keywords:
- IDebugProcess3::Execute
ms.assetid: d831cd81-d7bf-4172-8517-aa699867791f
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8b6647db9e3a013be0ffd3a0a12f92e9cb6cc738
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63405821"
---
# <a name="idebugprocess3execute"></a>IDebugProcess3::Execute
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このプロセスを停止状態から実行が続行されます。 (ステップ) など、以前の実行状態をクリアし、もう一度実行して、プロセスを開始します。  
  
> [!NOTE]
> このメソッドは、の代わりに使用する必要があります[Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Execute(  
   IDebugThread2* pThread  
);  
```  
  
```csharp  
int Execute(  
   IDebugThread2 pThread  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pThread`  
 [in][IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)スレッドの実行を表すオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="remarks"></a>Remarks  
 ユーザーは、他のプロセスのスレッドを停止状態から実行を起動するときに、このプロセスにこのメソッドが呼び出されます。 ユーザーが選択すると、このメソッドが呼び出されますも、**開始**コマンドから、**デバッグ**IDE のメニュー。 このメソッドの実装を呼び出す可能性があります、[再開](../../../extensibility/debugger/reference/idebugthread2-resume.md)プロセスの現在のスレッドでメソッド。  
  
> [!WARNING]
> 停止イベントまたは直接 (同期) イベントを送信しない[イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md); この呼び出しを処理中にそれ以外の場合、デバッガーがハングします。  
  
## <a name="see-also"></a>関連項目  
 [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)   
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [再開](../../../extensibility/debugger/reference/idebugthread2-resume.md)   
 [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
