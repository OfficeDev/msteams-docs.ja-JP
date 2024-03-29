---
title: タスク モジュール
author: surbhigupta
description: このモジュールでは、Microsoft Teams アプリからユーザーに情報を収集または表示するためのモーダル ポップアップ エクスペリエンスを追加する方法について説明します
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 23d6a0f1645fefe66544c755ddb617eba9ea8f3e
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035297"
---
# <a name="task-modules"></a>タスク モジュール

タスク モジュールを使用すると、Teams アプリケーションでモーダル ポップアップ エクスペリエンスを作成できます。 ポップアップでは、次のことができます。

* 独自のカスタム HTML または JavaScript コードを実行します。
* `<iframe>`YouTube やMicrosoft Streamビデオなどの -based ウィジェットを表示します。
* [アダプティブ カード](/adaptive-cards/)を表示します。

タスク モジュールは、タスクの開始と完了、ビデオや Power Business Intelligence (BI) ダッシュボードなどの豊富な情報の表示に役立ちます。 多くの場合、ポップアップ エクスペリエンスは、タブまたは会話ベースのボット エクスペリエンスと比較して、ユーザーがタスクを開始して完了する方が自然です。

タスク モジュールは、Microsoft Teams タブの基礎に基づいて構築されます。 これらは本質的に、ポップアップ ウィンドウ内のタブです。 これらは同じ SDK を使用するため、タブを構築している場合は、タスク モジュールの作成に既に精通しています。

タスク モジュールは次の 3 つの方法で呼び出すことができます。

* チャネルタブまたは個人用タブ: Microsoft Teams タブ SDK を使用すると、タブのボタン、リンク、またはメニューからタスク モジュールを呼び出すことができます。詳細については、 [タブでのタスク モジュールの使用に関するページを参照してください](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。
* ボット: ボットから送信された [カード](~/task-modules-and-cards/cards/cards-reference.md) のボタンを使用します。 これは、チャネル内のすべてのユーザーがボットで何をしているかを確認する必要がない場合に便利です。 たとえば、ユーザーがチャネル内の投票に応答する場合、そのポーリングが作成されているレコードを表示することは役に立ちません。 詳細については、 [Teams ボットのタスク モジュールの使用](~/task-modules-and-cards/task-modules/task-modules-bots.md)に関するページを参照してください。
* ディープ リンクから Teams の外部: どこからでもタスク モジュールを呼び出す URL を作成することもできます。 詳細については、 [タスク モジュールのディープ リンク構文に関するページを](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)参照してください。

## <a name="components-of-a-task-module"></a>タスク モジュールのコンポーネント

ボットから呼び出されたときのタスク モジュールの外観を次に示します。

:::image type="content" source="../assets/images/task-module/task-module-example.png" alt-text="タスク モジュールの例":::

タスク モジュールには、前の図に示すように次のものが含まれています。

1. アプリの [`color` アイコン](~/resources/schema/manifest-schema.md#icons)。
2. アプリの [`short` 名前](~/resources/schema/manifest-schema.md#name)。
3. [TaskInfo オブジェクト](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)のプロパティで`title`指定されたタスク モジュールのタイトル。
4. タスク モジュールの [閉じる] または [キャンセル] ボタン。 ユーザーがこのボタンを選択すると、アプリはイベントを `err` 受け取ります。 詳細については、 [タスク モジュールの結果を送信する例を](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)参照してください。

    > [!NOTE]
    > 現在、タスク モジュールがボットから呼び出されたときにイベントを検出 `err` することはできません。

5. 青い四角形は、[TaskInfo オブジェクト](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)のプロパティを使用して独自の Web ページを読み込む場合に`url`、Web ページが表示される場所です。 詳細については、「[タスク モジュールのサイズ策定](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing)」を参照してください。
6. [TaskInfo オブジェクト](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)のプロパティを使用してアダプティブ カードを`card`表示する場合は、パディングが追加されます。 詳細については、 [HTML または JavaScript タスク モジュールのタスク モジュール CSS に関するページ](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules)を参照してください。
7. **[サインアップ**] を選択すると、[アダプティブ カード] ボタンがレンダリングされます。 独自のページを使用する場合は、独自のボタンを作成します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [タスク モジュールを呼び出して閉じる](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="see-also"></a>関連項目

[カード](~/task-modules-and-cards/what-are-cards.md)
