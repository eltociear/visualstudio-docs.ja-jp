---
title: 'CA1716: 識別子はキーワード | と一致させることはできません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
helpviewer_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
ms.assetid: 900cc8a1-1089-4069-a4ce-10b109ac4fab
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f81aec5973d1915ba646c20c3b84186443678754
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669099"
---
# <a name="ca1716-identifiers-should-not-match-keywords"></a>CA1716: 識別子はキーワードと同一にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|IdentifiersShouldNotMatchKeywords|
|CheckId|CA1716|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 名前空間、型、または viritual またはインターフェイスのメンバーの名前が、プログラミング言語で予約されているキーワードと一致しています。

## <a name="rule-description"></a>規則の説明
 名前空間、型、および仮想およびインターフェイスのメンバーの識別子は、共通言語ランタイムを対象とする言語で定義されているキーワードと一致させることはできません。 使用されている言語とキーワードによっては、ライブラリを使用するのが困難になることがあります。

 このルールでは、次の言語のキーワードについて確認します。

- Visual Basic

- C#

- C++/CLI

  @No__t_0 キーワードには大文字と小文字を区別しない比較が使用され、その他の言語では大文字と小文字を区別する比較が使用されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 キーワードの一覧に表示されない名前を選択してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 識別子が API のユーザーと混同しないこと、および [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] で使用可能なすべての言語でライブラリが使用可能であることが確信できる場合は、この規則からの警告を抑制することができます。
