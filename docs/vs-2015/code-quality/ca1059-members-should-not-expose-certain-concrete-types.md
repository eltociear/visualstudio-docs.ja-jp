---
title: 'CA1059: メンバーは特定の具象型を公開できません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1059
- MembersShouldNotExposeCertainConcreteTypes
helpviewer_keywords:
- MembersShouldNotExposeCertainConcreteTypes
- CA1059
ms.assetid: 59f61f52-8d6c-49cb-aefb-191910523a3c
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4c105a1224c405d0be9d74ac6500c875df28604d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72604042"
---
# <a name="ca1059-members-should-not-expose-certain-concrete-types"></a>CA1059: メンバーは特定の具象型を公開できません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MembersShouldNotExposeCertainConcreteTypes|
|CheckId|CA1059|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 外部から参照できるメンバーは、特定の具象型であるか、そのパラメーターまたは戻り値のいずれかによって特定の具象型を公開します。 現在、このルールは次の具象型の露出を報告します。

- @No__t_0 から派生した型。

## <a name="rule-description"></a>規則の説明
 具象型は、完全な実装を含む型であるため、インスタンス化できます。 メンバーを広範囲に使用できるようにするには、具象型を提案されたインターフェイスに置き換えます。 これにより、インターフェイスを実装する任意の型をメンバーが受け入れることができるようになります。また、インターフェイスを実装する型が想定される場所で使用することもできます。

 次の表に、対象となる具象型とその推奨される置換の一覧を示します。

|具象型|Replacement|
|-------------------|-----------------|
|<xref:System.Xml.XPath.XPathDocument>|<xref:System.Xml.XPath.IXPathNavigable?displayProperty=fullName>.<br /><br /> インターフェイスを使用すると、XML データソースの特定の実装からメンバーを分離できます。|

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、具象型を提案されたインターフェイスに変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 具象型によって提供される特定の機能が必要な場合は、この規則からのメッセージを抑制することが安全です。

## <a name="related-rules"></a>関連規則
 [CA1011: 基本型をパラメーターとして渡すことを考慮します](../code-quality/ca1011-consider-passing-base-types-as-parameters.md)
