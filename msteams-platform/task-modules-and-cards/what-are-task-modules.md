---
title: タスク モジュール
author: surbhigupta
description: モーダル ポップアップ エクスペリエンスを追加して、アプリからユーザーに情報を収集または表示Microsoft Teamsします。
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3b0e639acc8901a3637189e435fcfc159e992ae3a674a437733474087103193c
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57707683"
---
# <a name="task-modules"></a>タスク モジュール

タスク モジュールを使用すると、アプリケーションでモーダル ポップアップ エクスペリエンスをTeamsできます。 ポップアップでは、次の方法を実行できます。

* 独自のカスタム HTML または JavaScript コードを実行します。
* `<iframe>`YouTube や Microsoft Stream ビデオなどの -based ウィジェットを表示します。
* アダプティブ カード [を表示します](/adaptive-cards/)。

タスク モジュールは、タスクの開始と完了、またはビデオや Power Business Intelligence (BI) ダッシュボードなどの豊富な情報の表示に役立ちます。 多くの場合、ポップアップ エクスペリエンスは、タブや会話ベースのボット エクスペリエンスと比較して、ユーザーがタスクを開始して完了する方が自然です。

タスク モジュールは、タブの基礎Microsoft Teamsします。 基本的には、ポップアップ ウィンドウ内のタブです。 同じ SDK を使用します。タブを作成している場合は、タスク モジュールの作成に慣れ親しまれています。

タスク モジュールは次の 3 つの方法で呼び出すことができます。

* チャネルまたは個人用タブ: タブ SDK Microsoft Teamsを使用して、タブのボタン、リンク、またはメニューからタスク モジュールを呼び出します。詳細については、「タブでのタスク[モジュールの使用」を参照してください](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。
* ボット: ボットから送信された [カードでボタン](~/task-modules-and-cards/cards/cards-reference.md) を使用する。 これは、チャネル内のすべてのユーザーがボットで何をしているのかを確認する必要が生じない場合に便利です。 たとえば、ユーザーがチャネル内のポーリングに応答する場合、そのポーリングのレコードが作成されているのを見るのは役に立ちます。 詳細については、「タスク モジュール[の使用」を参照Teamsしてください](~/task-modules-and-cards/task-modules/task-modules-bots.md)。
* ディープ リンクTeams外部: どこからでもタスク モジュールを呼び出す URL を作成できます。 詳細については、「タスク モジュールの [ディープ リンク構文」を参照してください](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)。

## <a name="components-of-a-task-module"></a>タスク モジュールのコンポーネント

ボットから呼び出された場合のタスク モジュールの外観を次に示します。

![タスク モジュールの例](~/assets/images/task-module/task-module-example.png)

タスク モジュールには、前の図に示すように、次の内容が含まれます。

1. アプリのアイコン[ `color` です](~/resources/schema/manifest-schema.md#icons)。
2. アプリ[ `short` の名前です](~/resources/schema/manifest-schema.md#name)。
3. TaskInfo オブジェクトのプロパティで指定 `title` されたタスク モジュール [のタイトル](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)です。
4. タスク モジュールの [閉じる] または [キャンセル] ボタン。 ユーザーがこのボタンを選択すると、アプリはイベントを受け取 `err` ります。 詳細については、タスク モジュール [の結果を送信する例を参照してください](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。

    > [!NOTE]
    > 現在、タスク モジュールがボットから呼び出された場合、イベント `err` を検出できない。

5. 青い四角形は、TaskInfo オブジェクトのプロパティを使用して独自の Web ページを読み込む場合に Web ページ `url` が [表示される場所です](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。 詳細については、「タスク モジュールの [サイズ変更」を参照してください](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-sizing)。
6. TaskInfo オブジェクトのプロパティを使用してアダプティブ カードを表示する場合 `card` [は](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) 、パディングが追加されます。 詳細については、「HTML または JavaScript タスク モジュールの [タスク モジュール CSS」を参照してください](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-css-for-html-or-javascript-task-modules)。
7. [サインアップ] を選択すると、アダプティブ カード ボタン **がレンダリングされます**。 独自のページを使用する場合は、独自のボタンを作成します。

## <a name="see-also"></a>関連項目

[カード](~/task-modules-and-cards/what-are-cards.md)

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [タスク モジュールを呼び出して閉じる](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
