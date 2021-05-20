---
title: コンテンツ ページを作成する
author: laujan
description: コンテンツ ページの作成方法
keywords: チーム タブ グループ の構成可能な静的
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 136160cb9154d62be40d8e29075ac1fc86135a6b
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566678"
---
# <a name="create-a-content-page-for-your-tab"></a>タブのコンテンツ ページを作成する

コンテンツ ページは、Teams クライアント内でレンダリングされる Web ページです。 通常、これらは以下の部分です。

* 個人スコープのカスタム タブ: この場合、コンテンツ ページはユーザーが最初に表示されるページです。
* チャンネル/グループのカスタムタブ: ユーザーがピンを設定し、適切なコンテキストでタブを構成すると、コンテンツページが表示されます。
* [タスクモジュール](~/task-modules-and-cards/what-are-task-modules.md): コンテンツページを作成し、それをタスクモジュール内の Web ビューとして埋め込むことができます。 ページはモーダル ポップアップの内部にレンダリングされます。

この記事は、コンテンツ ページをタブとして使用する場合に限定されています。ただし、ここでのガイダンスの大部分は、コンテンツ ページがエンド ユーザーにどのように表示されているかに関係なく適用されます。

## <a name="tab-content-and-design-guidelines"></a>タブの内容と設計ガイドライン

タブの全体的な目的は、実用的な価値と明らかな目的を持つ有意義で魅力的なコンテンツへのアクセスを提供することです。 これは、楽しいスタイルを見落とす必要があるという意味ではありませんが、タブデザインをクリーンにし、直感的で、コンテンツを没入感にすることで、混乱を最小限に抑えることに重点を置く必要があります。

詳細については、[タブデザインのガイドライン](~/tabs/design/tabs.md)および[Microsoft Teamsストア検証のガイドラインを](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)参照してください。

## <a name="integrate-your-code-with-teams"></a>コードをTeamsに統合する

ページをTeamsに表示するには[、Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)を含め、 `microsoftTeams.initialize()` ページの読み込み後に呼び出しを含める必要があります。 ページとTeams クライアントの通信方法は、次のとおりです。

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

### <a name="using-the-sdk-to-interact-with-teams"></a>SDK を使用したTeamsとの対話

[Teamsクライアント JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md)には、コンテンツ ページの開発に役立つ多くの追加機能が用意されています。

### <a name="deep-links"></a>ディープ リンク

Teams のエンティティへのディープ リンクを作成できます。 通常、これらは、タブ内のコンテンツや情報に移動するリンクを作成するために使用されます。詳細については、「 [Microsoft Teams でコンテンツおよび機能へのディープ リンクを作成する](~/concepts/build-and-test/deep-links.md)」を参照してください。

### <a name="task-modules"></a>タスクモジュール

タスク モジュールは、タブからトリガーできるモーダル ポップアップのようなエクスペリエンスです。通常、コンテンツ ページでは、ユーザーが複数のページ内を移動しないようにします。 代わりに、タスク モジュールを使用して、追加情報を収集したり、リスト内のアイテムの詳細を表示したり、その他の時間にユーザーに追加情報を表示したりするためのフォームを表示します。 タスクモジュール自体は、追加のコンテンツページにすることも、アダプティブカードを使用して完全に作成することもできます。 詳細については [、タブでのタスクモジュールの使用](~/task-modules-and-cards/task-modules/task-modules-tabs.md) を参照してください。

### <a name="valid-domains"></a>有効なドメイン

タブで使用されるすべての URL ドメインが `validDomains` [マニフェスト](~/concepts/build-and-test/apps-package.md)の配列に含まれていることを確認します。 詳細については、マニフェスト スキーマ リファレンスの [validDomain](~/resources/schema/manifest-schema.md#validdomains) を参照してください。 ただし、タブの中核機能はTeams内に存在し、Teamsの外には存在しないことに注意してください。

## <a name="reorder-static-personal-tabs"></a>静的な個人用タブの順序を変更する

マニフェストバージョン 1.7 以降では、開発者は個人用アプリのすべてのタブを並べ替えることができます。 特に、開発者は *ボット チャット* タブを移動できます。 予約済みの 2 つのタブ entityId キーワード、 *会話* 、および *についてが* 宣言されました。

*個人* スコープを持つボットを作成すると、既定で個人用アプリの最初のタブ位置に表示されます。 別の位置に移動する場合は、予約済みのキーワードである *会話* を使用して、静的タブオブジェクトをマニフェストに追加する必要があります。 *[会話*] タブは、配列内の [*会話*] タブを追加した場所に基づいて、Web またはデスクトップに表示されます `staticTabs` 。 

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

## <a name="show-a-native-loading-indicator"></a>ネイティブ読み込みインジケーターを表示する

マニフェスト[スキーマ v1.7](../../../resources/schema/manifest-schema.md)以降では、web コンテンツがTeamsに読み込まれる場所であれば、[ネイティブ読み込みインジケーター](../../../resources/schema/manifest-schema.md#showloadingindicator)を提供できます。 たとえば、 [タブコンテンツページ](#integrate-your-code-with-teams)、 [構成ページ](configuration-page.md)、 [削除ページ](removal-page.md)、 [タブのタスクモジュール](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)など。

> [!NOTE]
> * モバイル クライアントでの動作は、このマニフェスト プロパティでは構成できません。 モバイル クライアントは、コンテンツ ページと iframe ベースのタスク モジュール間で既定でネイティブ読み込みインジケーターを表示します。 モバイル上のこのインジケータは、コンテンツを取得する要求が行われ、要求が完了するとすぐに却下されたときに表示されます。
> * アプリ マニフェストで指定した場合  `"showLoadingIndicator : true`  は、すべてのタブ構成、コンテンツ、および削除ページとすべての iframe ベースのタスク モジュールが、以下の必須プロトコルに従う必要があります。

**積み込みインジケータを表示するには**

* `"showLoadingIndicator": true`マニフェストに追加します。 
* を呼び出すことを忘れないでください `microsoftTeams.initialize();` 。
* **オプション**: 画面に印刷する準備ができていて、アプリケーションの残りのコンテンツを遅延読み込みしたい場合は、手動で呼び出して読み込みインジケーターを非表示にすることができます。 `microsoftTeams.appInitialization.notifyAppLoaded();`
* **必須**: 最後 `microsoftTeams.appInitialization.notifySuccess()` に、アプリが正常に読み込まれたことをTeamsに通知する呼び出し。 Teamsは、該当する場合は、読み込みインジケーターを非表示にします。 `notifySuccess`30 秒以内に呼び出されない場合は、アプリがタイムアウトし、再試行オプションを含むエラー画面が表示されると見なされます。
* アプリケーションの読み込みに失敗した場合は、エラー `microsoftTeams.appInitialization.notifyFailure(reason);` があったことをTeamsに知らせるために呼び出すことができます。 エラー画面がユーザーに表示されます。

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
