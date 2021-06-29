---
title: コンテンツ ページを作成する
author: surbhigupta
description: コンテンツ ページを作成する方法
keywords: teams タブ グループ チャネル構成可能静的
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1276fdac2d3a30836b574b8e51b99fcbd7a415d2
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179735"
---
# <a name="create-a-content-page-for-your-tab"></a>タブのコンテンツ ページを作成する

コンテンツ ページは、クライアント内で表示されるTeamsです。 これらは、次の一部です。

* 個人用スコープのカスタム タブ: この場合、コンテンツ ページはユーザーが最初に表示するページです。
* チャネルまたはグループのカスタム タブ: コンテンツ ページは、ユーザーがピンで固定され、適切なコンテキストでタブを構成した後に表示されます。
* タスク [モジュール](~/task-modules-and-cards/what-are-task-modules.md): コンテンツ ページを作成し、タスク モジュール内に Web ビューとして埋め込む。 ページはモーダル ポップアップ内でレンダリングされます。

この記事では、コンテンツ ページをタブとして使用する方法について説明します。ただし、ここでのガイダンスの大部分は、コンテンツ ページがユーザーに提示される方法に関係なく適用されます。

## <a name="tab-content-and-design-guidelines"></a>タブのコンテンツとデザインのガイドライン

タブの全体的な目的は、実用的な価値と明らかな目的を持つ有意義で魅力的なコンテンツへのアクセスを提供します。 タブデザインをクリーンにし、直感的にナビゲーションし、コンテンツを没入感のあるものに集中する必要があります。

詳細については、「タブデザイン[ガイドライン」](~/tabs/design/tabs.md)および「ストアMicrosoft Teams[ガイドライン」を参照してください](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)。

## <a name="integrate-your-code-with-teams"></a>コードとコードを統合Teams

ページをページに表示するには、Teams [JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)クライアント SDK をMicrosoft Teamsし、ページの読み込み後に呼び出し `microsoftTeams.initialize()` を含める必要があります。 

次のコードは、ページとクライアントが通信する方法のTeams示しています。

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

## <a name="access-additional-content"></a>追加のコンテンツにアクセスする

SDK を使用して Teams を操作し、ディープ リンクを作成し、タスク モジュールを使用し、URL ドメインが配列に含まれているか確認することで、追加のコンテンツにアクセス `validDomains` できます。

### <a name="use-the-sdk-to-interact-with-teams"></a>SDK を使用してアプリを操作Teams

この[Teams JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md)には、コンテンツ ページの開発に役立つ機能が多数含まれています。

### <a name="deep-links"></a>ディープ リンク

Teams のエンティティへのディープ リンクを作成できます。 これらは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。詳細については、「コンテンツと機能[へのディープ リンク](~/concepts/build-and-test/deep-links.md)を作成する」を参照Teams。

### <a name="task-modules"></a>タスク モジュール

タスク モジュールは、タブからトリガーできるモーダル ポップアップ エクスペリエンスです。コンテンツ ページでは、タスク モジュールを使用して、追加の情報を収集したり、リスト内のアイテムの詳細を表示したり、追加情報をユーザーに提示したりするためにフォームを表示できます。 タスク モジュール自体は、追加のコンテンツ ページでも、アダプティブ カードを使用して完全に作成することもできます。 詳細については、「タブでのタスク [モジュールの使用」を参照してください](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。

### <a name="valid-domains"></a>有効なドメイン

タブで使用されている URL ドメインすべてがマニフェストの配列に含 `validDomains` まれているか確認 [します](~/concepts/build-and-test/apps-package.md)。 詳細については、マニフェスト スキーマ [リファレンスの validDomains](~/resources/schema/manifest-schema.md#validdomains) を参照してください。

> [!NOTE]
> タブのコア機能は、Teamsの外部ではなく、Teams。

## <a name="show-a-native-loading-indicator"></a>ネイティブ読み込みインジケーターの表示

マニフェスト スキーマ [v1.7](../../../resources/schema/manifest-schema.md)から、ネイティブ読み込みインジケーター [を指定できます](../../../resources/schema/manifest-schema.md#showloadingindicator)。 たとえば、タブ[コンテンツ ページ、](#integrate-your-code-with-teams)[構成ページ、](configuration-page.md)[削除ページ](removal-page.md)、タブ[内のタスク モジュールなどです](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。

> [!NOTE]
> * モバイル クライアントでの動作は、ネイティブ読み込みインジケーター プロパティでは構成できません。 モバイル クライアントは、コンテンツ ページと iframe ベースのタスク モジュール全体で既定でこのインジケーターを表示します。 モバイル上のこのインジケーターは、コンテンツの取得要求が行われたときに表示され、要求が完了するとすぐに却下されます。

アプリ マニフェストで指定する場合は、すべてのタブ構成、コンテンツ、および削除ページとすべての iframe ベースのタスク モジュールは、次の手順 `showLoadingIndicator : true`  に従う必要があります。

**読み込みインジケーターを表示する**

1. マニフェスト `"showLoadingIndicator": true` に追加します。
1. `microsoftTeams.initialize();` を呼び出します。
1. 必須の **手順として、** アプリが正常に読み込まれたTeamsを呼び出して通知 `microsoftTeams.appInitialization.notifySuccess()` します。 Teams場合は、読み込みインジケーターを非表示にしてください。 30 秒以内に呼び出されない場合は、アプリがタイム アウトし、再試行オプションが設定されたエラー画面 `notifySuccess`  が表示されます。
1. **必要に** 応じて、画面に印刷する準備が整い、アプリケーションの残りのコンテンツを遅延読み込みする場合は、呼び出しによって読み込みインジケーターを手動で非表示にできます `microsoftTeams.appInitialization.notifyAppLoaded();` 。
1. アプリケーションの読み込みに失敗した場合は、エラーが発生 `microsoftTeams.appInitialization.notifyFailure(reason);` Teamsを呼び出して確認できます。 エラー画面がユーザーに表示されます。 次のコードは、アプリケーションエラーの理由の例を示しています。

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="see-also"></a>関連項目

* [Teamsタブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [[チャネルまたはグループ] タブを作成する](~/tabs/how-to/create-channel-group-tab.md)
* [コンテンツ ページを作成する](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [構成ページを作成する](~/tabs/how-to/create-tab-pages/configuration-page.md)
