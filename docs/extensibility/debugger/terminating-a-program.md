---
title: プログラムの終了 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debugging [Debugging SDK], terminating a program
ms.assetid: eedda0a3-5e05-44fe-841d-a2f4866ac72d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f82a8238b542ce9aa9f5489df38553410e1326d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331358"
---
# <a name="terminating-a-program"></a>プログラムの終了
次のセクションでは、1 つのスレッドで 1 つのプログラムの終了について説明します。

## <a name="termination-process"></a>終了プロセス

1. DE 送信、 [IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)有効な[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)します。

2. DE 送信、 [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)有効な[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)します。

   IDE は、デザイン モードに入ります。 デバッグ エンジンまたはランタイム環境は[IDebugPortNotify2::RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)ポートからプログラムを削除します。

## <a name="see-also"></a>関連項目
- [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)