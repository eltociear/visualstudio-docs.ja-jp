---
title: 従来の言語サービスのインターフェイス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IVsLanguageInfo interface
- language services, objects
ms.assetid: 03b2d507-f463-417e-bc22-bdac68eeda52
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 02f63cd5e3f0599723aee12f7aed2c56b74c3249
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196098"
---
# <a name="legacy-language-service-interfaces"></a>従来の言語サービスのインターフェイス
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

特定のプログラミング言語がありますの言語サービスのインスタンスを 1 つだけで。 ただし、1 つの言語サービスでは、1 つ以上のエディターを使用できます。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 特定のエディターでの言語サービスを関連付けないでしません。 したがって、言語サービスの操作を要求するときに、パラメーターとして適切なエディターを識別する必要があります。  
  
## <a name="common-interfaces-associated-with-language-services"></a>言語サービスに関連付けられている共通のインターフェイス  
 エディターを呼び出して、言語サービスの取得<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>を適切な VSPackage にします。 ID (SID) がこの呼び出しで渡されたサービスは、要求されている言語サービスを識別します。  
  
 別のクラスの任意の数には、コア言語サービスのインターフェイスを実装できます。 ただし、一般的なアプローチは、1 つのクラスで、次のインターフェイスを実装するためには。  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageBlock> (省略可能)  
  
  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>すべての言語サービスでインターフェイスを実装する必要があります。 ローカライズされた言語、言語サービスと、colorizer を取得する方法に関連付けられているファイル名拡張子の名前など、言語サービスに関する情報を提供します。  
  
## <a name="additional-language-service-interfaces"></a>追加の言語サービスのインターフェイス  
 言語サービスでは、他のインターフェイスを提供できます。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] テキスト バッファーのインスタンスごとにこれらのインターフェイスの別のインスタンスを要求します。 そのため、独自のオブジェクトでこれらの各インターフェイスを実装する必要があります。 次の表では、テキスト バッファーのインスタンスごとに 1 つのインスタンスを必要とするインターフェイスを示します。  
  
|Interface|説明|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|ドロップダウン バーなどのコード ウィンドウの表示を管理します。 このインターフェイスを使用して取得できます、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>メソッド。 1 つである<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>コード ウィンドウごと。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>|言語のキーワードと区切り記号の色を付けます。 このインターフェイスを使用して取得できます、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>メソッド。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> 描画時に呼び出されます。 内の計算処理を要する作業を避ける<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>またはパフォーマンスが低下する可能性があります。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>|パラメーターの IntelliSense のツールヒントを提供します。 言語サービスは、そのメソッドのデータを示す文字にする必要がありますを認識すると、始めかっこなどが表示されますが呼び出す、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A>にテキストを通知するメソッドを表示する言語サービスは、パラメーター ヒントを表示できます。 テキスト ビューしを呼び出し、言語サービスのメソッドを使用して、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>ツールヒントを表示する、必要な情報を取得するインターフェイス。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>|IntelliSense ステートメント入力候補を提供します。 呼び出す言語サービスの入力候補一覧を表示する準備ができたら、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>テキスト ビューのメソッド。 テキスト ビュー、コールバックによって、言語サービスにメソッドを使用して、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>オブジェクト。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|コマンド ハンドラーを使用して、テキスト ビューの変更が可能です。 実装するクラス、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>インターフェイスを実装する必要がありますも、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>インターフェイス。 テキスト ビューを取得、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>オブジェクト クエリを実行して、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>オブジェクトに渡される、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>メソッド。 1 つあります<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>それぞれのビューのオブジェクト。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|ユーザーがコード ウィンドウに入力するコマンドを受け取ります。 出力を監視、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>実装がカスタムの完了の情報を提供し、変更を表示するには<br /><br /> 渡す、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>呼び出しのテキスト ビュー オブジェクト<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>します。|  
  
## <a name="see-also"></a>関連項目  
 [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)   
 [チェックリスト: 従来の言語サービスの作成](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)
