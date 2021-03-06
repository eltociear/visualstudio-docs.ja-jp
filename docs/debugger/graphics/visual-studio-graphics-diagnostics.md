---
title: グラフィックス診断 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.graphics
ms.assetid: fa69c550-62a7-41b5-bb1f-7eb04af1a6e8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e69d88bb5764836d82232cec26606009eaf694d7
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73187737"
---
# <a name="visual-studio-graphics-diagnostics"></a>Visual Studio グラフィックス診断
Visual Studio*グラフィックス診断*は、Direct3D アプリのレンダリングとパフォーマンスの問題を記録して分析するための一連のツールです。 グラフィックス診断は、Windows PC でローカルに実行されているアプリ、Windows デバイス エミュレーターで実行されているアプリ、あるいはリモート PC またはデバイスで実行されているアプリに対して使用できます。

 グラフィックス診断のワークフローは、アプリが Direct3D を使用する方法の記録を、アプリの実行中にライブでキャプチャすることから始まります。記録したアプリの動作は、直ちに分析し、共有し、後で使用するために保存できます。 キャプチャセッションは、Visual Studio から手動で開始したり、コマンドラインキャプチャツールの**ユーティリティ**を使用して手動で制御したりすることができます。 キャプチャセッションは、グラフィックス診断 capture Api を使用してプログラムで開始および制御することもできます。

 キャプチャ セッションによる記録が終わったら、Visual Studio の *Graphics Analyzer* を使用して、いつでもその内容を再生できます。その際、アプリが使用したのと正確に同じリソースとレンダリング コマンドを使用して、キャプチャされたフレームが再作成されます。 次に、Graphics Analyzer ウィンドウに用意されているツールを使用して、キャプチャされたフレームを詳細に分析できます。 これらのツールを使用して、任意の Direct3D API 呼び出し、リソース、パイプライン状態オブジェクト、パイプライン ステージ、またはキャプチャしたフレーム内の任意のピクセルの完全な履歴さえも、調べることができます。 これらのツールを連携して使用すれば、レンダリングの問題を直感的に調査できます。キャプチャされたフレームにその問題が現れた地点から始めて、アプリのソース コード、シェーダー、またはグラフィックス アセットにある根本原因にまで掘り下げていきます。

 パフォーマンスの問題を診断するには、キャプチャしたフレームを*フレーム分析*ツールを使用して分析できます。 このツールは、アプリが Direct3D を使用する方法を自動的に変更して、さらに最適なパフォーマンスを実現できないかどうか探索し、すべてのバリエーションのベンチマークを提供します。 以前は、このような変更を手動で設定してベンチマークを取り、いちばん違いの大きいものを見つけるだけでした。 フレーム分析を利用する場合は、有効であることが既に分かっている変更を加える必要があるだけです。

 グラフィックス診断は、Direct3D アプリの外観を視覚的に優れたものにし、パフォーマンスを最大にするために役立ちます。

 Visual Studio グラフィックス診断で提供される内容の詳細については、 [「概要」](overview-of-visual-studio-graphics-diagnostics.md)を参照してください。

## <a name="in-this-section"></a>このセクションの内容
 [概要](overview-of-visual-studio-graphics-diagnostics.md)グラフィックス診断のワークフローとツールについて説明します。

 [はじめに](getting-started-with-visual-studio-graphics-diagnostics.md)このセクションでは、Visual Studio グラフィックス診断をインストールする方法と、Direct3D アプリでグラフィックス診断の使用を開始する方法について説明します。

 [グラフィックス情報のキャプチャ](capturing-graphics-information.md)グラフィックス診断を使用してアプリのレンダリングの問題を調査するには、まず、アプリが DirectX を使用する方法に関する情報を記録します。 アプリが通常どおりに実行されているときの記録セッション中に関心があるフレームを "*キャプチャ*" (つまり、選択) します。 キャプチャには、フレームがレンダリングされる方法に関する詳細情報が含まれています。 キャプチャした情報をグラフィックス ログのドキュメントとして保存し、後で調べたり、チームの他のメンバーと共有したりできます。

 [GPU 使用率](../../profiling/gpu-usage.md)グラフィックス診断を使用してアプリをプロファイリングするには、GPU 使用率ツールを使用します。 GPU 使用率ツールを、CPU 使用率など、他のプロファイリング ツールと連携して使用すると、アプリのパフォーマンスの問題を引き起こしている可能性のある CPU および GPU のアクティビティを、問題と関連付けることができます。

 [グラフィックスログドキュメント](graphics-log-document.md)記録されたグラフィックスログの確認を開始するには、グラフィックスログのドキュメントウィンドウを使用して、キャプチャしたフレーム (または特定のピクセル) を選択します。これにより、影響を受ける*イベント*(つまり、DirectX API 呼び出し) を詳細に確認できます。

 [フレーム分析](graphics-frame-analysis.md)フレームを選択した後、グラフィックスフレーム分析を使用して、レンダリングのパフォーマンスを確認し、調整します。

 [イベント一覧](graphics-event-list.md)フレームを選択したら、 **[グラフィックスイベント一覧]** を使用してイベントを調べ、レンダリングの問題に関連しているかどうかを判断します。

 [状態](graphics-state.md)[状態] ウィンドウは、現在のイベントの時点でアクティブになっているグラフィックスの状態を理解するのに役立ちます。

 [パイプラインステージ](graphics-pipeline-stages.md) **[グラフィックスパイプラインステージ]** ウィンドウで、現在選択されているイベントがグラフィックスパイプラインの各ステージによってどのように処理されるかを調査します。これにより、レンダリングの問題が最初に表示される場所を特定できます。 パイプライン ステージの調査は、正しくない変換のためにオブジェクトが表示されない場合、または次のステージで期待される出力と一致しない出力が 1 つのステージで生成された場合に特に便利です。

 [イベント呼び出し履歴](graphics-event-call-stack.md) **[グラフィックスイベント呼び出し履歴]** を使用して、現在選択されているイベントの呼び出し履歴を調べ、レンダリングの問題に関連するアプリコードに移動できるようにします。

 [ピクセル履歴](graphics-pixel-history.md) **[グラフィックスピクセル履歴]** ウィンドウを使用して、現在選択されているピクセルが影響を受けるイベントによってどのように影響を受けているかを分析することで、特定の種類のレンダリングの問題を引き起こしているイベントまたはイベントの組み合わせを特定できます。 ピクセル履歴は、ピクセル シェーダー出力が正しくないか、フレーム バッファーと不適切に組み合わされているためにオブジェクトが正しくレンダリングされない場合、または、オブジェクトのピクセルがフレーム バッファーに到達する前に破棄されているためにオブジェクトが表示されない場合に特に便利です。

 [オブジェクトテーブル](graphics-object-table.md)**グラフィックスオブジェクトテーブル**を使用して、現在選択されているイベントに対して有効な特定の Direct3D オブジェクトとリソースのプロパティと内容を確認します。 オブジェクト テーブルを使用すると、イベントの発生時にアクティブであるグラフィックス デバイス コンテキストを特定し、定数バッファー、頂点バッファー、テクスチャなどのグラフィックス リソースの内容を調べることが容易になります。

 [HLSL デバッガー](hlsl-shader-debugger.md)現在選択されているイベントおよびグラフィックスパイプラインステージのシェーダーコードがどのように動作するかを調べるには、 **HLSL デバッガー**を使用してコードをステップ実行し、変数の内容を確認して、その他の一般的なデバッグタスクを実行します。 また、結果がグラフィックス パイプラインによってさらに処理されるか、アプリによって再び読み取られるかに関係なく、HLSL デバッガーを使用して計算シェーダー コードを調べることができます。

 [コマンドラインキャプチャツール](command-line-capture-tool.md)コマンドラインキャプチャツールを使用すると、Visual Studio またはプログラムによるキャプチャを使用せずに、グラフィックス情報をすばやくキャプチャして再生できます。 具体的には、オートメーションを行う場合や、テスト環境でコマンド ライン キャプチャ ツールを使用できます。

 [例](graphics-diagnostics-examples.md)いくつかの例では、グラフィックス診断ツールを使用して、さまざまな種類のレンダリングの問題を診断する方法を示します。

## <a name="related-sections"></a>関連項目

| Title | 説明 |
| - | - |
| [デバッガー機能ツアー](../debugger-feature-tour.md) | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のデバッグ機能を紹介します。 |
| [DirectX のグラフィックスとゲーム](/windows/win32/directx) | DirectX グラフィックスの手法を説明する文書を提供します。 |
