---
title: '方法: プログラムによってワークシートを保護する'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- protection, adding to worksheets
- documents [Office development in Visual Studio], document protection
- document protection, adding to worksheets
- worksheets, protecting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 931bfba9aeac76132ca2dd5e6115abef9869a1df
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254589"
---
# <a name="how-to-programmatically-protect-worksheets"></a>方法: プログラムによってワークシートを保護する
  Microsoft Office Excel の保護機能を使用すると、ユーザーやコードがワークシート内のオブジェクトを編集できないようにすることができます。 既定では、保護を有効にすると、すべてのセルがロックされます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 ドキュメント レベルのカスタマイズでは、Excel デザイナーを使用してワークシートを保護できます。 プロジェクトの種類に関係なく、実行時にプログラムを使用してワークシートを保護することもできます。

> [!NOTE]
> 保護されているワークシートの領域に Windows フォーム コントロールを追加することはできません。

## <a name="use-the-designer"></a>デザイナーを使用する

### <a name="to-protect-a-worksheet-in-the-designer"></a>デザイナーでワークシートを保護するには

1. **[レビュー]** タブの **[変更]** グループで、 **[シートの保護]** をクリックします。

    **[シートの保護]** ダイアログボックスが表示されます。 パスワードを設定し、必要に応じて、セルの書式設定や行の挿入など、ワークシートでユーザーに実行を許可する特定のアクションを指定できます。

   保護されたワークシート内の特定の範囲の編集を、ユーザーに許可することもできます。

### <a name="to-allow-editing-in-specific-ranges"></a>特定の範囲の編集を許可するには

1. **[レビュー]** タブの **[変更]** グループで、 **[範囲の編集をユーザーに許可する]** をクリックします。

     **[範囲の編集をユーザーに許可する]** ダイアログボックスが表示されます。 パスワードを使用してロックを解除できる範囲と、パスワードがなくても範囲を編集できるユーザーを指定できます。

## <a name="use-code-at-run-time"></a>実行時にコードを使用する
 次のコードは、(ユーザーから取得したパスワードを格納する変数 getPasswordFromUser を使用して) パスワードを設定し、並べ替えだけを許可します。

### <a name="to-protect-a-worksheet-by-using-code-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで、コードを使用してワークシートを保護するには

1. ワークシートの <xref:Microsoft.Office.Tools.Excel.Worksheet.Protect%2A> メソッドを呼び出します。 この例では、 `Sheet1`という名前のワークシートを操作していると仮定します。

     [!code-csharp[Trin_VstcoreExcelAutomation#27](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#27)]
     [!code-vb[Trin_VstcoreExcelAutomation#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#27)]

### <a name="to-protect-a-worksheet-by-using-code-in-a-vsto-add-in"></a>VSTO アドインで、コードを使用してワークシートを保護するには

1. 作業中のワークシートの <xref:Microsoft.Office.Interop.Excel._Worksheet.Protect%2A> メソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#17](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#17)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#17](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#17)]

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: プログラムによってワークシートから保護を削除する](../vsto/how-to-programmatically-remove-protection-from-worksheets.md)
- [方法: プログラムによってブックを保護する](../vsto/how-to-programmatically-protect-workbooks.md)
- [方法: プログラムによってワークシートを非表示にする](../vsto/how-to-programmatically-hide-worksheets.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ワークシートホスト項目](../vsto/worksheet-host-item.md)
- [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
