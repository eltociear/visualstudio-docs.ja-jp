---
title: 'CA1810: 参照型の静的フィールドをインラインで初期化します |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- InitializeReferenceTypeStaticFieldsInline
- CA1810
helpviewer_keywords:
- InitializeReferenceTypeStaticFieldsInline
- CA1810
ms.assetid: e9693118-a914-4efb-9550-ec659d8d97d2
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9032ac105477370477b13554afe4ee65bd7cd733
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72609018"
---
# <a name="ca1810-initialize-reference-type-static-fields-inline"></a>CA1810: 参照型の静的フィールドをインラインで初期化します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|InitializeReferenceTypeStaticFieldsInline|
|CheckId|CA1810|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 参照型は、明示的な静的コンストラクターを宣言します。

## <a name="rule-description"></a>規則の説明
 型で明示的な静的コンストラクターを宣言すると、Just-In-Time (JIT) コンパイラが、静的コンストラクターが呼び出されたことを確認するために、型の静的メソッドと静的インスタンス コンストラクターに個別にチェックを追加します。 静的初期化は、静的メンバーにアクセスするか、型のインスタンスが作成されるときにトリガーされます。 ただし、静的な初期化は、型の変数を宣言しても使用しない場合にはトリガーされません。これは、初期化がグローバル状態を変更した場合に重要になる可能性があります。

 すべての静的データがインラインで初期化され、明示的な静的コンストラクターが宣言されていない場合、Microsoft 中間言語 (MSIL) コンパイラによって、`beforefieldinit` フラグと、静的データを初期化する暗黙の静的コンストラクターが MSIL 型に追加されます。カスタム. JIT コンパイラが `beforefieldinit` フラグを検出した場合、ほとんどの場合、静的コンストラクターチェックは追加されません。 静的フィールドにアクセスする前に、静的メソッドまたはインスタンスコンストラクターが呼び出される前に静的初期化が行われることは保証されていません。 静的な初期化は、型の変数が宣言された後でいつでも発生する可能性があることに注意してください。

 静的コンストラクターのチェックによってパフォーマンスが低下することがあります。 静的コンストラクターは、静的フィールドの初期化にのみ使用されることがよくあります。その場合は、静的フィールドに最初にアクセスする前に静的初期化が行われるようにする必要があります。 @No__t_0 の動作は、これらおよびその他のほとんどの型に適しています。 これは、静的な初期化がグローバル状態に影響し、次のいずれかに該当する場合にのみ不適切です。

- グローバルな状態への影響は高価であり、型が使用されていない場合は必要ありません。

- グローバル状態の効果には、型の静的フィールドにアクセスせずにアクセスできます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、静的データが宣言されたとき、および静的コンストラクターを削除するときに、静的データをすべて初期化します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 パフォーマンスが問題にならない場合は、このルールの警告を抑制しても安全です。または、静的な初期化によって発生するグローバル状態の変更がコストがかかる場合や、型の静的メソッドが呼び出される前に発生することを保証する必要がある場合、または型のインスタンスが作成される場合は、。

## <a name="example"></a>例
 次の例では、ルールに違反する型 `StaticConstructor` が使用されています。この型は、規則に適合するように静的コンストラクターをインライン初期化に置き換える、`NoStaticConstructor` の型です。

 [!code-csharp[FxCop.Performance.RefTypeStaticCtor#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.RefTypeStaticCtor/cs/FxCop.Performance.RefTypeStaticCtor.cs#1)]
 [!code-vb[FxCop.Performance.RefTypeStaticCtor#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.RefTypeStaticCtor/vb/FxCop.Performance.RefTypeStaticCtor.vb#1)]

 @No__t_1 クラスの MSIL 定義に `beforefieldinit` フラグが追加されていることに注意してください。

 **. class public auto Ansi staticconstructor**では、 **[mscorlib] system.object が拡張**され、**クラス staticconstructor 
 クラスの末尾にある**
 **{** 
} が拡張さ**れます。クラスパブリック自動 ansi beforefieldinit nostaticconstructor** **[mscorlib] System.object**の 
 **{** 1 **}//End クラスの nostaticconstructor を**拡張します
## <a name="related-rules"></a>関連規則
 [CA2207: 値型の静的フィールドのインラインを初期化します](../code-quality/ca2207-initialize-value-type-static-fields-inline.md)
