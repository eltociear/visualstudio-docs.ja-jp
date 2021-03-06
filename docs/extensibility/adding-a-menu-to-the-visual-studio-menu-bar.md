---
title: Visual Studio のメニュー バーにメニューを追加する |Microsoft Docs
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- menus, creating top level
- top-level menus
ms.assetid: 58fc1a31-2aeb-441c-8e48-c7d5cbcfe501
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a28e7f69ed8e9a76e11d8892ee677435f75c99b2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349788"
---
# <a name="add-a-menu-to-the-visual-studio-menu-bar"></a>Visual Studio のメニュー バー メニューに追加します。

このチュートリアルでは、Visual Studio 統合開発環境 (IDE) のメニュー バーにメニューを追加する方法を示します。 IDE のメニュー バーには、**ファイル**、**編集**、**ビュー**、**ウィンドウ**、および**ヘルプ**のようなメニュー項目が含まれています。

Visual Studio のメニュー バーに新しいメニューを追加する前に、コマンドは、既存のメニュー内に配置する必要があるかどうかを検討してください。 コマンド配置の詳細については、次を参照してください。 [Visual Studio のメニューとコマンド](../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)します。

メニューが宣言されている、 *.vsct*プロジェクトのファイル。 メニューの詳細については、 *.vsct*ファイルを参照してください[コマンド、メニューのおよびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)します。

このチュートリアルを完了すると、という名前のメニューを作成することができます**TestMenu** 1 つのコマンドを格納しています。

> [!NOTE]
> VS の 2019年で拡張機能によって提供された、最上位メニューがの下に配置、**拡張**メニュー。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降、ダウンロード センターから Visual Studio SDK をインストールすることはできません。 これは Visual Studio のセットアップにオプション機能として含まれるようになりました。 また、後から VS SDK をインストールすることもできます。 詳細については、"[Visual Studio SDK をインストール](../extensibility/installing-the-visual-studio-sdk.md)"を参照してください。

## <a name="create-a-vsix-project-that-has-a-custom-command-item-template"></a>カスタム コマンド項目テンプレートを持つ VSIX プロジェクトを作成します。

1. という名前の VSIX プロジェクトを作成する`TopLevelMenu`します。 VSIX プロジェクト テンプレートを見つけることができます、**新しいプロジェクト**ダイアログで"vsix"を検索します。  詳細については、次を参照してください。[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)します。

2. という名前のカスタム コマンド項目テンプレートを追加、プロジェクトが開いたら、 **TestCommand**します。 **ソリューション エクスプ ローラー**でプロジェクト ノードを右クリックし、選択**追加** >  **新しい項目の**します。 **新しい項目の追加**ダイアログ ボックスに移動して**Visual c#/機能拡張**選択と**カスタム コマンド**。 **名前**ウィンドウの下部にあるフィールドに、コマンド ファイル名を変更して*TestCommand.cs*します。

## <a name="create-a-menu-on-the-ide-menu-bar"></a>IDE のメニュー バーにメニューを作成します。

::: moniker range="vs-2017"

1. **ソリューション エクスプ ローラー**オープン*TestCommandPackage.vsct*します。

    ファイルの最後では、\<シンボル > いくつか含まれているノード\<GuidSymbol > ノード。 GuidTestCommandPackageCmdSet という名前のノード、としては、次のように、新しいシンボルを追加します。

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. 空の作成\<メニュー > 内のノード、\<コマンド > ノード、直前に\<グループ >。 \<メニュー > ノードを追加、\<メニュー > 次のように、ノード。

   ```xml
   <Menus>
         <Menu guid="guidTestCommandPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
           <Parent guid="guidSHLMainMenu"
                   id="IDG_VS_MM_TOOLSADDINS" />
           <Strings>
             <ButtonText>TestMenu</ButtonText>
             <CommandName>TestMenu</CommandName>
           </Strings>
       </Menu>
   </Menus>
   ```

    `guid`と`id`コマンド セットで、コマンド セットと、特定のメニューにメニューの値が指定されます。

    `guid`と`id`親の値は、ツールとアドインのメニューを含む Visual Studio のメニュー バーのセクションに、メニューを配置します。

    値、`CommandName`文字列は、メニュー項目のテキストが表示されることを指定します。

3. \<グループ > セクションで、検索、\<グループ > を変更して、\<親 > 要素を追加したメニューをポイントします。

   ```csharp
   <Groups>
         <Group guid="guidTestCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTestCommandPackageCmdSet" id="TopLevelMenu"/>
         </Group>
       </Groups>
   ```

    これにより、新しいメニューのグループの一部です。

::: moniker-end

::: moniker range=">=vs-2019"

1. **ソリューション エクスプ ローラー**オープン*TopLevelMenuPackage.vsct*します。

    ファイルの最後では、\<シンボル > いくつか含まれているノード\<GuidSymbol > ノード。 GuidTopLevelMenuPackageCmdSet という名前のノード、としては、次のように、新しいシンボルを追加します。

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. 空の作成\<メニュー > 内のノード、\<コマンド > ノード、直前に\<グループ >。 \<メニュー > ノードを追加、\<メニュー > 次のように、ノード。

   ```xml
   <Menus>
         <Menu guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
           <Parent guid="guidSHLMainMenu"
                   id="IDG_VS_MM_TOOLSADDINS" />
           <Strings>
             <ButtonText>TestMenu</ButtonText>
             <CommandName>TestMenu</CommandName>
           </Strings>
       </Menu>
   </Menus>
   ```

    `guid`と`id`コマンド セットで、コマンド セットと、特定のメニューにメニューの値が指定されます。

    `guid`と`id`親の値は、ツールとアドインのメニューを含む Visual Studio のメニュー バーのセクションに、メニューを配置します。

    値、`CommandName`文字列は、メニュー項目のテキストが表示されることを指定します。

3. \<グループ > セクションで、検索、\<グループ > を変更して、\<親 > 要素を追加したメニューをポイントします。

   ```csharp
   <Groups>
         <Group guid="guidTopLevelMenuPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu"/>
         </Group>
       </Groups>
   ```

    これにより、新しいメニューのグループの一部です。

::: moniker-end

4. 検索、`Buttons`セクション。 注意、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]パッケージ テンプレートが生成、`Button`をその親に設定を持つ要素`MyMenuGroup`します。 その結果、このコマンドは、メニューに表示されます。

## <a name="build-and-test-the-extension"></a>ビルドし、テストの拡張機能

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスのインスタンスが表示されます。

::: moniker range="vs-2017"

2. 実験用インスタンスのメニュー バーを含める必要があります、 **TestMenu**メニュー。

::: moniker-end

::: moniker range=">=vs-2019"

2. **拡張**実験用インスタンスのメニューに含める必要があります、 **TestMenu**メニュー。

::: moniker-end

3. **TestMenu**  メニューのをクリックして**テスト コマンドを呼び出す**します。

     メッセージ ボックスが表示され、"TestCommand パッケージ内で TopLevelMenu.TestCommand.MenuItemCallback()"メッセージを表示する必要があります。

## <a name="see-also"></a>関連項目

- [コマンド、メニューのおよびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)