---
title: 'CA1414: ブール型の P-Invoke 引数を MarshalAs | でマークします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1414
- MarkBooleanPInvokeArgumentsWithMarshalAs
helpviewer_keywords:
- CA1414
- MarkBooleanPInvokeArgumentsWithMarshalAs
ms.assetid: c0c84cf5-7701-4897-9114-66fc4b895699
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 588e16a6b21b320ad7012bd20d79a62d027679e3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652693"
---
# <a name="ca1414-mark-boolean-pinvoke-arguments-with-marshalas"></a>CA1414: ブール型の P/Invoke 引数を MarshalAs に設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkBooleanPInvokeArgumentsWithMarshalAs|
|CheckId|CA1414|
|カテゴリ|Microsoft. 相互運用性|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 プラットフォーム呼び出しメソッドの宣言に <xref:System.Boolean?displayProperty=fullName> パラメーターまたは戻り値が含まれていますが、<xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=fullName> 属性がパラメーターまたは戻り値に適用されていません。

## <a name="rule-description"></a>規則の説明
 プラットフォーム呼び出しメソッドはアンマネージコードにアクセスし、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] または <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> の `Declare` キーワードを使用して定義されます。 <xref:System.Runtime.InteropServices.MarshalAsAttribute> は、マネージコードとアンマネージコードの間でデータ型を変換するために使用されるマーシャリング動作を指定します。 @No__t_0 や <xref:System.Int32?displayProperty=fullName> など、多くの単純なデータ型は、アンマネージコードで1つの表現を持ち、マーシャリング動作の指定は必要ありません。共通言語ランタイムは、自動的に正しい動作を提供します。

 @No__t_0 データ型には、アンマネージコード内の複数の表現があります。 @No__t_0 が指定されていない場合、<xref:System.Boolean> データ型の既定のマーシャリング動作は <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName> ます。 これは32ビットの整数であり、すべての状況に適しているわけではありません。 アンマネージメソッドによって必要とされるブール値は、適切な <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName> と一致している必要があります。 Unmanagedtype.bool は、常に4バイトの Win32 BOOL 型です。 @No__t_1 またはその他の 1 C++バイト型には unmanagedtype.bool を使用する必要があります。 詳細については、「[ブール型の既定のマーシャリング](https://msdn.microsoft.com/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)」を参照してください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、<xref:System.Boolean> パラメーターまたは戻り値に <xref:System.Runtime.InteropServices.MarshalAsAttribute> を適用します。 属性の値を適切な <xref:System.Runtime.InteropServices.UnmanagedType> に設定します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 既定のマーシャリング動作が適切な場合でも、動作が明示的に指定されていれば、コードをより簡単に管理できます。

## <a name="example"></a>例
 次の例は、適切な <xref:System.Runtime.InteropServices.MarshalAsAttribute> 属性でマークされている2つのプラットフォーム呼び出しメソッドを示しています。

 [!code-cpp[FxCop.Interoperability.BoolMarshalAs#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/cpp/FxCop.Interoperability.BoolMarshalAs.cpp#1)]
 [!code-csharp[FxCop.Interoperability.BoolMarshalAs#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/cs/FxCop.Interoperability.BoolMarshalAs.cs#1)]
 [!code-vb[FxCop.Interoperability.BoolMarshalAs#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/vb/FxCop.Interoperability.BoolMarshalAs.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1901: P/Invoke 宣言はポータブルでなければなりません](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)

 [CA2101: P/Invoke 文字列引数に対してマーシャリングを指定します](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

## <a name="see-also"></a>参照
 [アンマネージコードとの相互運用](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)[を行うブール型に対する既定のマーシャリングの](https://msdn.microsoft.com/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>
