---
title: '方法: プログラムによってワークシートでスペルをチェックします。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- spellchecking
- spelling checker, worksheets
- worksheets, checking spelling
- spelling, checking in worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: feb284657932a0c20cd785b14db5e2b3de9366f1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62575565"
---
# <a name="how-to-programmatically-check-spelling-in-worksheets"></a>方法: プログラムによってワークシートでスペルをチェックします。
  ワークシート内の単語のスペルをプログラムでチェックすることができます。 ワークシート内の単語のスペルが正しくないと、 **[スペル チェック]** ダイアログ ボックスが自動的に表示されます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-check-spelling-in-a-worksheet-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズでワークシート内のスペルをチェックするには

1. ワークシートの <xref:Microsoft.Office.Tools.Excel.Worksheet.CheckSpelling%2A> メソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomation#45](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#45)]
     [!code-vb[Trin_VstcoreExcelAutomation#45](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#45)]

## <a name="to-check-spelling-in-a-worksheet-in-a-vsto-add-in"></a>VSTO アドインでワークシート内のスペルをチェックするには

1. 作業中のワークシートの <xref:Microsoft.Office.Interop.Excel._Worksheet.CheckSpelling%2A> メソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#22](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#22)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#22](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#22)]

## <a name="see-also"></a>関連項目
- [ワークシートを操作します。](../vsto/working-with-worksheets.md)
- [方法: Excel の計算をプログラムで実行します。](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
