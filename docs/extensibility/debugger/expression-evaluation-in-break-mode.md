---
title: 中断モードでの式の評価 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, expression evaluation
- debugging [Debugging SDK], expression evaluation
- expression evaluation, break mode
ms.assetid: 34fe5b58-15d5-4387-a266-72120f90a4b6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af231333981697705ba58fe505b0bf55304b8287
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353837"
---
# <a name="expression-evaluation-in-break-mode"></a>中断モードでの式の評価
次のセクションでは、デバッガーが中断モードであり、式の評価を実施する必要があるときに発生するプロセスについて説明します。

## <a name="expression-evaluation-process"></a>式の評価プロセス
 式の評価に関連する基本的な手順を次に示します。

1. セッション デバッグ マネージャー (SDM) を呼び出す[IDebugStackFrame2::GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) 、式のコンテキストのインターフェイスを取得する[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)します。

2. SDM を呼び出して[IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)を解析する文字列。

3. ParseText は S_OK を返しますが、エラーの理由が返されます。

     それ以外の場合

     ParseText は S_OK を返さない場合、SDM 呼び出すことができますし、 [IDebugExpression2::EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)または[IDebugExpression2::EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)解析された式から最終的な値を取得します。

    - 使用する場合`IDebugExpression2::EvaluateSync`、指定されたコールバック インターフェイスが評価の継続的なプロセスを通信します。 最終的な値が返される、 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)インターフェイス。

    - 使用する場合`IDebugExpression2::EvaluateAsync`、指定されたコールバック インターフェイスが評価の継続的なプロセスを通信します。 評価が完了したら、EvaluateAsync 送信、 [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)コールバック インターフェイス。 このイベント インターフェイスの最終的な値の結果で[GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)します。

## <a name="see-also"></a>関連項目
- [デバッガー イベントを呼び出す](../../extensibility/debugger/calling-debugger-events.md)