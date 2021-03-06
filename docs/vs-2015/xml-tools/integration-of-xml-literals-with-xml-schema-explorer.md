---
title: Xml リテラルと XML スキーマエクスプローラーの統合 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 57a29998-c6e8-48ac-bdb0-5788e73f9164
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a15767454c83604de2844e4c0a9f2e121a9a1a4f
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75846122"
---
# <a name="integration-of-xml-literals-with-xml-schema-explorer"></a>XML リテラルと XML スキーマ エクスプローラーの統合
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Basic では XML リテラルがサポートされているため、Visual Basic コードに XML フラグメントを直接組み込むことができます。 詳細については、「 [XML リテラルの概要](https://msdn.microsoft.com/library/bb384629.aspx)」を参照してください。

 Visual Basic プロジェクトの XSD ファイルに XML リテラルが含まれる場合、XML スキーマ エクスプローラーで XML スキーマ セットを表示できます。 XML リテラルに関連付けられているスキーマセットを表示するには、xml リテラルまたは XML 名前空間インポートで XML ノードを右クリックし、 **[スキーマエクスプローラーで表示]** を選択します。

 ![XML リテラルを Visual Basic します。XML スキーマエクスプローラー](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer1.gif "VBXMLLiteralsWithXMLSchemaExplorer1")

 これにより、XML スキーマ エクスプローラーが Visual Basic ファイルと並んで表示されます。

 ![XML リテラルを Visual Basic します。XML スキーマエクスプローラー](../xml-tools/media/vbxmlliteralswithxmlschemaexplorer2.gif "VBXMLLiteralsWithXMLSchemaExplorer2")

 この機能は Visual Studio 2008 SP1 で導入されました。 この機能の詳細については、「 [Channel 9 インタビュー: Visual Studio 2008 SP1 の XML スキーマエクスプローラー](https://channel9.msdn.com/Blogs/funkyonex/XML-Schema-Explorer-in-Visual-Studio-2008-SP1)」を参照してください。

## <a name="see-also"></a>参照
 [方法: XML リテラルに XML スキーマ デザイナーを使用する](../xml-tools/how-to-use-the-xml-schema-designer-with-xml-literals.md)
