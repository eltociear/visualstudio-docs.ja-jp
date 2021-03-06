---
title: メソッドにパラメーターを追加するクイック アクション
ms.date: 09/28/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 6720421fd5188688214665d85de682542b1c1357
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595866"
---
# <a name="add-a-parameter-to-a-method-using-a-quick-action"></a>クイック アクションを使用してメソッドにパラメーターを追加する

このコード生成は以下に適用されます。

- C#

- Visual Basic

**概要:** 使用量に基づいて、メソッドにパラメーターを自動的に追加することができます。

**条件:** メソッドにパラメーターを追加し、それを自動的に正しく宣言する必要がある場合。

**理由:** 呼び出す前にメソッドの宣言にパラメーターを追加することもできますが、この機能ではそれがメソッドの呼び出しに基づいて自動的に追加されます。

## <a name="how-to-use-it"></a>使用方法

1. メソッドの呼び出しに追加の引数を追加します。

   呼び出す場所で、メソッドの名前の下に赤い波線が表示されます。

2. [クイック アクション] メニューが表示されるまで赤い波線の上にポインターを合わせます。 [クイック アクション] メニューの**下矢印**を選択した後、 **[パラメーターを [メソッド] に追加する]** を選択します。

   ![Visual Studio でのメソッドにパラメーターを追加するクイック アクション](media/add-parameter-to-method.png)

   > [!TIP]
   > また、[クイック アクション] メニューにアクセスするには、メソッドの呼び出しの行にカーソルを合わせて **Ctrl**+ **.** キーを押すか、 (ピリオド)、または、ファイルの余白の電球アイコンを選択するという方法もあります。

   Visual Studio によって、メソッドの宣言に新しいパラメーターが追加されます。

> [!NOTE]
> メソッドに対するその他の呼び出しがある場合、このクイック アクションを使用した後はそれらでエラーが発生する場合があります。新しく追加されたパラメーターの引数を指定していないためです。

## <a name="see-also"></a>関連項目

- [コンストラクターにパラメーターを追加する](generate-constructor.md#addparameter)
