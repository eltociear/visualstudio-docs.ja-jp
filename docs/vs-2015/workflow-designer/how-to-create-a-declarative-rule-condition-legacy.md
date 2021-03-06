---
title: '方法: 宣言型の規則条件を作成する (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- declarative rule conditions
- condition statements, declarative rule conditions
- Rule Condition Editor dialog box
ms.assetid: 804b6129-c433-408f-a424-46987967730c
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0c23fed64d7f3a7681fce96663262f6d633299a9
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75849331"
---
# <a name="how-to-create-a-declarative-rule-condition-legacy"></a>方法: 宣言的ルール条件を作成する (レガシ)
このトピックでは、[!INCLUDE[wfd1](../includes/wfd1-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする従来の [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用してルール条件を宣言する方法について説明します。

 条件ステートメントは、 **True**または**False**に評価されます。 宣言型のルール条件とは、[[ルール条件エディター] ダイアログボックス (レガシ)](../workflow-designer/rule-condition-editor-dialog-box-legacy.md)を使用して作成され、ワークフローと共に XML として格納される condition ステートメントです。 複数の述語を結合したブール値演算とワークフロー ステートとを比較する述語を含めることができます。

 宣言的ルール条件は、次のような Windows Workflow Foundation 事前定義アクティビティで使用されます。

- [ConditionedActivityGroup](https://msdn2.microsoft.com/library/system.workflow.activities.conditionedactivitygroup.aspx)

- [IfElseBranchActivity](https://msdn2.microsoft.com/library/system.workflow.activities.ifelsebranchactivity.aspx)

- [ReplicatorActivity](https://msdn2.microsoft.com/library/system.workflow.activities.replicatoractivity.aspx)

- [WhileActivity](https://msdn2.microsoft.com/library/system.workflow.activities.whileactivity.aspx)

- [SequentialWorkflowActivity](https://msdn2.microsoft.com/library/system.workflow.activities.sequentialworkflowactivity.aspx)

- [StateMachineWorkflowActivity](https://msdn2.microsoft.com/library/system.workflow.activities.statemachineworkflowactivity.aspx)

### <a name="to-create-a-declarative-rule-condition-using-the-rule-condition-editor"></a>ルール条件エディタを使って宣言的ルール条件を作成するには

1. アクティビティの **[プロパティ]** ウィンドウで、アクティビティに応じて **[条件]** **プロパティまたは**[期間] プロパティをクリックします。

2. プロパティの一覧から **[宣言型の規則の条件]** を選択します。

3. **[条件]** または 発生する **[条件]** プロパティを展開します。

4. **[Conditionname]** プロパティをクリックします。

5. **[Conditionname]** の省略記号 **[...]** をクリックして、 **[条件の選択]** ダイアログボックスを開きます。

6. **[新しい条件]** をクリックして、 **[ルール条件エディター]** ダイアログボックスを開きます。

7. **[条件]** ボックスに条件の式を入力します。

     条件式の作成方法の詳細については、「[[ルール条件エディター] ダイアログボックス (レガシ)](../workflow-designer/rule-condition-editor-dialog-box-legacy.md)」を参照してください。

8. 条件式の作成が終了したら、 **[OK]** をクリックしてダイアログボックスを閉じ、名前が割り当てられたルール条件を作成します。

     **[条件の選択**] ダイアログボックスが表示されます。

     **[条件の選択**] ダイアログボックスの使用方法の詳細については、「 [[条件の選択] ダイアログボックス (レガシ)](../workflow-designer/select-condition-dialog-box-legacy.md)」を参照してください。

## <a name="see-also"></a>参照
 [レガシワークフローアクティビティ](../workflow-designer/legacy-workflow-activities.md) [ConditionedActivityGroup を](https://msdn2.microsoft.com/library/bb675237.aspx)使用した[IfElseBranchActivity アクティビティ](https://msdn2.microsoft.com/library/bb628465.aspx)[の使用 [](https://msdn2.microsoft.com/library/bb628544.aspx) [While](https://msdn2.microsoft.com/library/bb628552.aspx)アクティビティ[ルール条件エディター] ダイアログボックス (レガシ)](../workflow-designer/rule-condition-editor-dialog-box-legacy.md) [[条件の選択] ダイアログボックス (レガシ](../workflow-designer/select-condition-dialog-box-legacy.md))[ワークフロー内の条件](https://msdn2.microsoft.com/library/bb628447.aspx)の使用
