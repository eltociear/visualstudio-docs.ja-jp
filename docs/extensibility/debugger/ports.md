---
title: ポート |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports
- debugging [Debugging SDK], ports
ms.assetid: 1d7f3aa7-7eff-4cab-bc53-0a566b1a9363
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f925bda151809bb4554fcfed7f46131d51a25179
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351522"
---
# <a name="ports"></a>ポート
デバッガーのアーキテクチャで、*ポート*:

- サーバーで実行する一連のプロセスのコンテナー。 たとえば、ポートは、シリアル ケーブルで Windows CE ベース デバイスまたは DCOM 以外のネットワークに接続されたマシンへの接続を表すことができます。 ローカルのポートと呼ばれる 1 つの特殊なポートには、ローカル コンピューターで実行されているすべてのプロセスが含まれています。

- 名前または識別子自体を識別できます。

- できますとポートで実行されているすべてのプロセスを列挙し、起動し、これらのプロセスを終了します。

- によって表される、 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)インターフェイスを渡すことによって作成される、 [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)引数[AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)します。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] すべて Windows ベースのプロセス、ネイティブおよびマネージの両方を処理する既定のポートを提供します。 カスタム ポートは Windows ベースではない外部のデバイスとの接続を設定する必要があります。 このようなカスタム ポートを指定するもカスタム ポートのサプライヤーを設定する必要があります。

## <a name="see-also"></a>関連項目
- [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [プロセス](../../extensibility/debugger/processes.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)
- [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)