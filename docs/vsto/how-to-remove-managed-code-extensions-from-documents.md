---
title: '方法: マネージコード拡張をドキュメントから削除する'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- managed code extensions [Office development in Visual Studio], removing
- documents [Office development in Visual Studio], managed code extensions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0832f0e404331e68fe88dfc990c51ed699eca263
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985793"
---
# <a name="how-to-remove-managed-code-extensions-from-documents"></a>方法: マネージコード拡張をドキュメントから削除する
  Microsoft Office Word または Microsoft Office Excel のドキュメントレベルのカスタマイズの一部であるドキュメントまたはブックから、プログラムによってカスタマイズアセンブリを削除できます。 その後、ユーザーはドキュメントを開いて内容を表示できますが、ドキュメントに追加したカスタムユーザーインターフェイス (UI) は表示されず、コードは実行されません。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 カスタマイズアセンブリを削除するには、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]によって提供される `RemoveCustomization` メソッドのいずれかを使用します。 どの方法を使用するかは、実行時にカスタマイズを削除するか (Word 文書または Excel ブックが開いているときにカスタマイズでコードを実行するか)、閉じられたドキュメントまたは自分が作成したドキュメントからカスタマイズを削除するかどうかによって異なります。Microsoft Office がインストールされていないサーバー上の。

## <a name="to-remove-the-customization-assembly-at-run-time"></a>実行時にカスタマイズアセンブリを削除するには

1. カスタマイズコードで、<xref:Microsoft.Office.Tools.Word.Document.RemoveCustomization%2A> メソッド (Word の場合) または <xref:Microsoft.Office.Tools.Excel.Workbook.RemoveCustomization%2A> メソッド (Excel の場合) を呼び出します。 このメソッドは、カスタマイズが不要になった後にのみ呼び出す必要があります。

     コード内でこのメソッドを呼び出す場所は、カスタマイズの使用方法によって異なります。 たとえば、ユーザーがドキュメントそのものだけを必要とする他のクライアント (カスタマイズではない) にドキュメントを送信する準備が整うまで、カスタマイズの機能を使用する場合は、顧客がクリックしたときに `RemoveCustomization` を呼び出す UI を提供できます。 また、カスタマイズによってドキュメントが最初に開かれたときにデータを入力する場合でも、ユーザーが直接アクセスする他の機能がカスタマイズによって提供されない場合は、カスタマイズしてすぐに RemoveCustomization を呼び出すことができます。ドキュメントの初期化を終了します。

## <a name="to-remove-the-customization-assembly-from-a-closed-document-or-a-document-on-a-server"></a>閉じられたドキュメントまたはサーバー上のドキュメントからカスタマイズアセンブリを削除するには

1. コンソールアプリケーションや Windows フォームプロジェクトなど、Microsoft Office を必要としないプロジェクトでは、VisualStudio アセンブリへの参照を追加します。 *ServerDocument*アセンブリです。

2. 次の**Imports**ステートメントまたは**using**ステートメントをコードファイルの先頭に追加します。

     [!code-csharp[Trin_VstcoreDeployment#1](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#1)]
     [!code-vb[Trin_VstcoreDeployment#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#1)]

3. <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスの静的 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> メソッドを呼び出し、パラメーターのソリューションドキュメントパスを指定します。

     次のコード例では、デスクトップ上にある*worddocument1.docx*という名前のドキュメントからカスタマイズを削除することを前提としています。

     [!code-csharp[Trin_VstcoreDeployment#2](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#2)]
     [!code-vb[Trin_VstcoreDeployment#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#2)]

4. プロジェクトをビルドし、カスタマイズを削除するコンピューターでアプリケーションを実行します。 コンピューターには、Visual Studio 2010 Tools for Office runtime がインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [ServerDocument クラスを使用してサーバー上のドキュメントを管理する](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [方法: マネージコード拡張機能をドキュメントにアタッチする](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
