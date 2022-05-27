---
title: コンテンツ ページを作成する
author: surbhigupta
description: コンテンツ ページを作成する方法
keywords: Teams タブ グループ チャネル構成可能スタティック
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 8de792faafeaa526a1abffe042394daeeb60cb3d
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757473"
---
# <a name="create-a-content-page-for-your-tab"></a>タブのコンテンツ ページを作成する

コンテンツ ページは、Teams クライアント内でレンダリングされる Web ページです。これは次の一部です。

* 個人用スコープのカスタム タブ: この場合、コンテンツ ページはユーザーが最初に見つけるページです。
* チャネルまたはグループのカスタム タブ: コンテンツページは、ユーザーが適切なコンテキストでタブをピン留めし、構成した後に表示されます。
* [タスク モジュール](~/task-modules-and-cards/what-are-task-modules.md): コンテンツ ページを作成し、タスク モジュール内に Web ビューとして埋め込むことができます。 ページはモーダル ポップアップ内にレンダリングされます。

この記事は、コンテンツ ページをタブとして使用する場合に固有です。ただし、ここでのガイダンスのほとんどは、コンテンツ ページがユーザーに表示される方法に関係なく適用されます。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="tab-content-and-design-guidelines"></a>タブのコンテンツとデザインのガイドライン

タブの全体的な目的は、実用的な価値と明確な目的を持つ意味のある魅力的なコンテンツへのアクセスを提供することです。 

タブデザインをクリーンにし、ナビゲーションを直感的に操作し、コンテンツをイマーシブなものにすることに集中する必要があります。詳細については、[タブデザインのガイドライン](~/tabs/design/tabs.md)と[ストアの検証ガイドラインMicrosoft Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)参照してください。

## <a name="integrate-your-code-with-teams"></a>コードを Teams と統合する

Teams でページを表示するには、[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) を含め、ページの読み込み後に `app.initialize()` の呼び出しを含める必要があります。

次のコードは、ページと Teams クライアントの通信方法の例を示しています。

# <a name="teamsjs-v2"></a>[TeamsJS v2](#tab/teamsjs-v2)

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v2.0.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    app.initialize();
    </script>
...
</body>
```

# <a name="teamsjs-v1"></a>[TeamsJS v1](#tab/teamsjs-v1)

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.10.0/js/MicrosoftTeams.min.js'></script>
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

***

## <a name="access-additional-content"></a>追加のコンテンツにアクセスする

SDK を使用して Teams と対話し、ディープ リンクを作成し、タスク モジュールを使用して、URL ドメインが `validDomains` 配列に含まれているかどうかを確認することで、追加のコンテンツにアクセスできます。

### <a name="use-the-sdk-to-interact-with-teams"></a>SDK を使用して Teams と対話する

[Teams クライアント JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) には、コンテンツ ページの開発時に役立つ多くの追加機能が用意されています。

### <a name="deep-links"></a>ディープ リンク

Teams のエンティティへのディープ リンクを作成できます。 これらは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。詳細については、「[Teamsのコンテンツと機能へのディープ リンクを作成する](~/concepts/build-and-test/deep-links.md)」を参照してください。

### <a name="task-modules"></a>タスク モジュール

タスク モジュールは、タブからトリガーできるモーダル ポップアップ エクスペリエンスです。コンテンツ ページで、タスク モジュールを使用して、追加情報の収集、リスト内のアイテムの詳細の表示、または追加情報をユーザーに表示するためのフォームを表示します。 タスク モジュール自体は、追加のコンテンツ ページにすることも、アダプティブ カードを使用して完全に作成することもできます。 詳細については、「[タブでタスク モジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-tabs.md)」 を参照してください。

### <a name="valid-domains"></a>有効なドメイン

タブで使用されるすべての URL ドメインが、[マニフェスト](~/concepts/build-and-test/apps-package.md) の `validDomains` 配列に含まれていることを確認します。 詳細については、「マニフェスト スキーマリファレンスの[validDomains](~/resources/schema/manifest-schema.md#validdomains)」 を参照してください。

> [!NOTE]
> タブの主要な機能は Teams 内に存在し、Teams の外部には存在しません。

## <a name="show-a-native-loading-indicator"></a>ネイティブ読み込みインジケーターの表示

[マニフェスト スキーマ v1.7](../../../resources/schema/manifest-schema.md) 以降では、[native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) を指定できます。 たとえば、[タブ コンテンツ ページ](#integrate-your-code-with-teams)、[構成ページ](configuration-page.md)、[削除ページ](removal-page.md)、および [タブのタスク モジュール](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。

> [!NOTE]
>
> * モバイル クライアントでの動作は、ネイティブ読み込みインジケーター プロパティを使用して構成することはできません。 モバイル クライアントでは、コンテンツ ページと iframe ベースのタスク モジュール全体で、このインジケーターが既定で表示されます。 モバイル上のこのインジケーターは、コンテンツをフェッチする要求が行われたときに表示され、要求が完了するとすぐに無視されます。

アプリ マニフェストで `showLoadingIndicator : true` を指定した場合、すべてのタブ構成、コンテンツ、削除ページ、およびすべての iframe ベースのタスク モジュールは、次の手順に従う必要があります。

読み込みインジケーターを表示する方法:

1. マニフェストに `"showLoadingIndicator": true` を追加します。
1. `app.initialize();` を呼び出します。
1. **必須** ステップとして、`app.notifySuccess()` を呼び出して、アプリが正常に読み込まれたことを Teams に通知します。 次に、読み込みインジケーター Teams非表示にします (該当する場合)。 30 秒以内に呼び出されない場合`notifySuccess`、Teamsはアプリがタイムアウトしたことを前提とし、再試行オプションを使用してエラー画面を表示します。
1. **必要に応じて**、画面に印刷する準備が整い、アプリケーションの残りのコンテンツを遅延読み込む場合は、読み込みインジケーターを呼び出 `app.notifyAppLoaded();`して手動で非表示にすることができます。
1. アプリケーションが読み込まれない場合は、呼び出`app.notifyFailure({reason: app.FailedReason.Timeout, message: "failure message"});`してエラーについてTeamsに知らせ、必要に応じてエラー メッセージを入力できます。 エラー画面がユーザーに表示されます。 次のコードは、アプリケーションの読み込みに失敗した場合に示すことができる理由を定義する列挙体を示しています。

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [構成ページを作成する](~/tabs/how-to/create-tab-pages/configuration-page.md)

## <a name="see-also"></a>関連項目

* [Teams タブ](~/tabs/what-are-tabs.md)
* [プライベート タブを作成する](~/tabs/how-to/create-personal-tab.md)
* [タブのリンクの展開とステージ ビュー](~/tabs/tabs-link-unfurling.md)
* [構成ページを作成する](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [Microsoft Teams タブの DevTools](~/tabs/how-to/developer-tools.md)
