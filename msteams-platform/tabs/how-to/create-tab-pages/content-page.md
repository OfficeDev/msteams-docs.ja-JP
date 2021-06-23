---
title: コンテンツ ページを作成する
author: surbhigupta
description: コンテンツ ページを作成する方法
keywords: teams タブ グループ チャネル構成可能静的
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: abb073cee4a9417ee4a9f095acdbe18c5e6d7713
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068524"
---
# <a name="create-a-content-page-for-your-tab"></a>タブのコンテンツ ページを作成する

コンテンツ ページは、クライアント内で表示されるTeamsです。 通常、これらは次の一部です。

* 個人用スコープのカスタム タブ: この例では、コンテンツ ページはユーザーが最初に見つけ入るページです。
* チャネル/グループ のカスタム タブ: ユーザーが適切なコンテキストでタブをピンで固定して構成すると、コンテンツ ページが表示されます。
* タスク [モジュール](~/task-modules-and-cards/what-are-task-modules.md): コンテンツ ページを作成し、タスク モジュール内に Web ビューとして埋め込む。 モーダル ポップアップ内にページが表示されます。

この記事では、コンテンツ ページをタブとして使用する方法について説明します。ただし、ここでのガイダンスの大部分は、コンテンツ ページがエンド ユーザーに提示される方法に関係なく適用されます。

## <a name="tab-content-and-design-guidelines"></a>タブのコンテンツとデザインのガイドライン

タブの全体的な目的は、実用的な価値と明らかな目的を持つ有意義で魅力的なコンテンツへのアクセスを提供する必要があります。 これは、快適なスタイルを見送る必要があるという意味ではありません。タブデザインをクリーンにし、ナビゲーションを直感的に行い、コンテンツを没入感のあるものにすることで、混乱を最小限に抑えることに集中する必要があります。

詳細については、「タブデザインガイドライン[」](~/tabs/design/tabs.md)および「ストア検証[Microsoft Teams」を参照してください。](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)

## <a name="integrate-your-code-with-teams"></a>コードとコードを統合Teams

ページをページに表示するには、Teams [JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)クライアント SDK をMicrosoft Teamsし、ページの読み込み後に呼び出し `microsoftTeams.initialize()` を含める必要があります。 ページとクライアントが通信Teams方法は次の通り。

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    microsoftTeams.initialize();
    </script>
...
</body>
```

## <a name="accessing-additional-content"></a>追加コンテンツへのアクセス

### <a name="using-the-sdk-to-interact-with-teams"></a>SDK を使用してユーザーと対話Teams

この[Teams JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md)には、コンテンツ ページの開発に役立つ機能が多数含まれています。

### <a name="deep-links"></a>ディープ リンク

Teams のエンティティへのディープ リンクを作成できます。 通常、これらは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。詳細については、「コンテンツと機能[へのディープ リンク](~/concepts/build-and-test/deep-links.md)を作成する」を参照Microsoft Teams。

### <a name="task-modules"></a>タスク モジュール

タスク モジュールは、タブからトリガーできるモーダル ポップアップのようなエクスペリエンスです。通常、コンテンツ ページでは、複数のページを介してユーザーを移動する必要があります。 代わりに、タスク モジュールを使用して、追加情報の収集、リスト内のアイテムの詳細の表示、またはユーザーに追加情報を提示する必要があるその他の時間を表示するためのフォームを提示します。 タスク モジュール自体は、追加のコンテンツ ページでも、アダプティブ カードを使用して完全に作成することもできます。 詳細については [、「タブでのタスク モジュールの使用](~/task-modules-and-cards/task-modules/task-modules-tabs.md) 」を参照してください。

### <a name="valid-domains"></a>有効なドメイン

タブで使用されているすべての URL ドメインがマニフェストの配列に含 `validDomains` まれているか確認 [します](~/concepts/build-and-test/apps-package.md)。 詳細については、マニフェスト スキーマ [リファレンスの validDomains](~/resources/schema/manifest-schema.md#validdomains) を参照してください。 ただし、タブのコア機能は、タブの外部ではなく、Teams内に存在Teams。

## <a name="reorder-static-personal-tabs"></a>静的な個人用タブの並べ替え

マニフェスト バージョン 1.7 から、開発者は個人用アプリ内のすべてのタブを再配置できます。 特に、開発者はボット チャットタブを移動できます。これは常に既定で最初の位置に、個人用アプリのタブ ヘッダー内の任意の場所に移動できます。 2 つの予約済みタブ entityId キーワード、会話 *、およびについて* 宣言 *しました*。

個人用スコープを持つボットを *作成* すると、既定では個人用アプリの最初のタブ位置に表示されます。 別の位置に移動する場合は、予約キーワードである会話を使用して静的タブ オブジェクトをマニフェストに追加する必要 *があります*。 [ *会話* ] タブは、配列に [会話] タブを追加した場所に基づいて *Web* またはデスクトップに表示 `staticTabs` されます。 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

## <a name="show-a-native-loading-indicator"></a>ネイティブ読み込みインジケーターの表示

マニフェスト スキーマ[v1.7](../../../resources/schema/manifest-schema.md)から、Web コンテンツ[](../../../resources/schema/manifest-schema.md#showloadingindicator)がアプリケーションに読み込まれる場所を問Teams。 たとえば、タブ[コンテンツ ページ、](#integrate-your-code-with-teams)[構成ページ、](configuration-page.md)[削除ページ](removal-page.md)、タブ[内のタスク モジュールなどです](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。

> [!NOTE]
> * モバイル クライアントでの動作は、このマニフェスト プロパティでは構成できません。 モバイル クライアントは、コンテンツ ページと iframe ベースのタスク モジュール間で既定でネイティブ読み込みインジケーターを表示します。 モバイル上のこのインジケーターは、コンテンツの取得要求が行われたときに表示され、要求が完了するとすぐに却下されます。
> * アプリ マニフェストで指定した場合は、すべてのタブ構成、コンテンツ、および削除ページとすべての iframe ベースのタスク モジュールは、以下の必須プロトコルに従う  `"showLoadingIndicator : true`  必要があります。

**読み込みインジケーターを表示する**

* マニフェスト `"showLoadingIndicator": true` に追加します。 
* を呼び出す `microsoftTeams.initialize();` 必要があります。
* **オプション**: 画面に印刷する準備が整い、アプリケーションのコンテンツの残りの部分を遅延読み込みする場合は、呼び出しによって読み込みインジケーターを手動で非表示にできます `microsoftTeams.appInitialization.notifyAppLoaded();`
* **必須 :** 最後に、アプリが正常に読み込Teamsを呼び出して通知 `microsoftTeams.appInitialization.notifySuccess()` します。 Teams場合、読み込みインジケーターが非表示になります。 30 秒以内に呼び出されない場合は、アプリがタイム アウトし、再試行オプション付きエラー画面が  `notifySuccess`  表示されます。
* アプリケーションの読み込みに失敗した場合は、エラーが発生 `microsoftTeams.appInitialization.notifyFailure(reason);` Teamsを呼び出して確認できます。 次に、エラー画面がユーザーに表示されます。

    ```typescript
    ``
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```
    >
