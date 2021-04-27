---
title: コンテンツ ページを作成する
author: laujan
description: コンテンツ ページを作成する方法
keywords: teams タブ グループ チャネル構成可能静的
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 9dc6c73d877d9355c5d4a9653e0d8ed669fb347e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020381"
---
# <a name="create-a-content-page-for-your-tab"></a>タブのコンテンツ ページを作成する

コンテンツ ページは、Teams クライアント内でレンダリングされる Web ページです。 通常、これらは次の一部です。

* 個人用スコープのカスタム タブ - このインスタンスでは、コンテンツ ページはユーザーが最初に表示するページです。
* チャネル/グループ のカスタム タブ - ユーザーが適切なコンテキストでタブをピンで固定して構成すると、コンテンツ ページが表示されます。
* タスク [モジュール](~/task-modules-and-cards/what-are-task-modules.md) - コンテンツ ページを作成し、それをタスク モジュール内の Web ビューとして埋め込みできます。 モーダル ポップアップ内にページが表示されます。

この記事では、コンテンツ ページをタブとして使用する方法について説明します。ただし、ここでのガイダンスの大部分は、コンテンツ ページがエンド ユーザーに提示される方法に関係なく適用されます。

## <a name="tab-content-and-style-guidelines"></a>タブのコンテンツとスタイルのガイドライン

タブの全体的な目的は、実用的な価値と明らかな目的を持つ有意義で魅力的なコンテンツへのアクセスを提供する必要があります。 これは、快適なスタイルを見送る必要があるという意味ではありません。タブデザインをクリーンにし、ナビゲーションを直感的に行い、コンテンツを没入感のあるものにすることで、混乱を最小限に抑えることに集中する必要があります。 タブと Microsoft Teams [アプリ承認プロセスの](~/tabs/design/tabs.md) ガイダンスを使用して、コンテンツと会話を [一度に表示する](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)

## <a name="integrate-your-code-with-teams"></a>コードを Teams と統合する

Teams にページを表示するには [、Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) クライアント SDK を含め、ページの読み込み後に呼び `microsoftTeams.initialize()` 出しを含める必要があります。 ページと Teams クライアントが通信する方法は次の通りです。

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

### <a name="using-the-sdk-to-interact-with-teams"></a>SDK を使用した Teams の操作

[Teams クライアント JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md)には、コンテンツ ページの開発に役立つ機能が多数含まれています。

### <a name="deep-links"></a>ディープ リンク

Teams のエンティティへのディープ リンクを作成できます。 通常、これらは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。「Microsoft [Teams でコンテンツと機能へのディープ リンクを作成する」を参照してください](~/concepts/build-and-test/deep-links.md)。

### <a name="task-modules"></a>タスク モジュール

タスク モジュールは、タブからトリガーできるモーダル ポップアップのようなエクスペリエンスです。通常、コンテンツ ページでは、複数のページを介してユーザーを移動する必要があります。 代わりに、タスク モジュールを使用して、追加情報の収集、リスト内のアイテムの詳細の表示、またはユーザーに追加情報を提示する必要があるその他の時間を表示するためのフォームを提示します。 タスク モジュール自体は、追加のコンテンツ ページでも、アダプティブ カードを使用して完全に作成することもできます。 詳細については [、「タブでのタスク モジュールの使用](~/task-modules-and-cards/task-modules/task-modules-tabs.md) 」を参照してください。

### <a name="valid-domains"></a>有効なドメイン

タブで使用されているすべての URL ドメインがマニフェストの配列に含 `validDomains` まれているか確認 [します](~/concepts/build-and-test/apps-package.md)。 詳細については、マニフェスト スキーマ [リファレンスの validDomains](~/resources/schema/manifest-schema.md#validdomains) を参照してください。 ただし、タブのコア機能は Teams 内に存在し、Teams の外部には存在しません。

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

マニフェスト スキーマ[v1.7](../../../resources/schema/manifest-schema.md)から、Web コンテンツ[](../../../resources/schema/manifest-schema.md#showloadingindicator)が Teams に読み込まれる場所 (タブ コンテンツ ページ、構成ページ、[](configuration-page.md)タブ内の[](removal-page.md)削除ページ、タスク モジュールなど) にネイティブ読み込みインジケーターを提供[できます](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。 [](#integrate-your-code-with-teams)

> [!NOTE]
> 1. モバイル クライアントでの動作は、このマニフェスト プロパティでは構成できません。 モバイル クライアントは、コンテンツ ページと iframe ベースのタスク モジュール間で既定でネイティブ読み込みインジケーターを表示します。 モバイル上のこのインジケーターは、コンテンツの取得要求が行われたときに表示され、要求が完了するとすぐに却下されます。
> 2. アプリ マニフェストで指定した場合は、すべてのタブ構成、コンテンツ、および削除ページとすべての iframe ベースのタスク モジュールは、以下の必須プロトコルに従う  `"showLoadingIndicator : true`  必要があります。


1. 読み込みインジケーターを表示するには、マニフェスト `"showLoadingIndicator": true` に追加します。 
2. を呼び出す `microsoftTeams.initialize();` 必要があります。
3. **オプション**。 画面に印刷する準備が整い、アプリケーションの残りのコンテンツを遅延読み込みする場合は、呼び出しによって読み込みインジケーターを手動で非表示にできます `microsoftTeams.appInitialization.notifyAppLoaded();`
4. **必須です**。 最後に、アプリが `microsoftTeams.appInitialization.notifySuccess()` 正常に読み込まれたと Teams に通知する呼び出しを行います。 該当する場合、Teams は読み込みインジケーターを非表示にします。 30 秒以内に呼び出されない場合は、アプリがタイム アウトし、再試行オプション付きエラー画面が  `notifySuccess`  表示されます。
5. アプリケーションの読み込みに失敗した場合は、Teams にエラー `microsoftTeams.appInitialization.notifyFailure(reason);` が発生したと知らせる呼び出しを行います。 次に、エラー画面がユーザーに表示されます。

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
