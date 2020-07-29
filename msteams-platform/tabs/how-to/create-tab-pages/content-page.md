---
title: コンテンツ ページを作成する
author: laujan
description: ''
keywords: teams タブグループチャネルの構成可能な静的
ms.topic: conceptual
ms.author: v-laujan
ms.openlocfilehash: 49cd771c45bc3c4f91a7ab5f38beaf01da712544
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434490"
---
# <a name="create-a-content-page-for-your-tab"></a>タブのコンテンツページを作成する

コンテンツページは、Teams クライアント内でレンダリングされる web ページです。 通常は、次の一部です。

* このインスタンスでは、個人を対象範囲とするカスタムタブ。コンテンツページは、ユーザーが最初に検出したページです。
* チャネル/グループカスタムタブ-ユーザーが適切なコンテキストでタブを固定して構成すると、[コンテンツ] ページが表示されます。
* [タスクモジュール](~/task-modules-and-cards/what-are-task-modules.md)-コンテンツページを作成し、それをタスクモジュール内の webview として埋め込むことができます。 ページはモーダルポップアップ内にレンダリングされます。

この記事では、コンテンツページをタブとして使用する方法について説明します。ただし、ここに示すガイダンスの大部分は、エンドユーザーにコンテンツページを表示する方法に関係なく適用されます。

## <a name="tab-content-and-style-guidelines"></a>タブの内容とスタイルのガイドライン

タブの全体的な目的は、実用的な価値と明確な目的を持つ、有意義で魅力的なコンテンツへのアクセスを提供することです。 見栄えの良いスタイルを先送りする必要があるわけではありませんが、タブデザインをすっきりさせ、ナビゲーションを直観的に、コンテンツのイマーシブ化を行うことによって、乱雑さを最小化することを重視する必要があります。 タブおよび[Microsoft Teams アプリ承認プロセスガイダンス](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)[を使用して、コンテンツと会話を一度にすべて](~/tabs/design/tabs.md)表示

## <a name="integrate-your-code-with-teams"></a>コードを Teams と統合する

ページを Teams に表示するには、 [Microsoft Teams の JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest)を含み、ページの読み込み後にの呼び出しを含める必要があり `microsoftTeams.initialize()` ます。 ページと Teams クライアントが通信する方法は次のとおりです。

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

## <a name="accessing-additional-content"></a>その他のコンテンツへのアクセス

### <a name="using-the-sdk-to-interact-with-teams"></a>SDK を使用して Teams を操作する

[Teams クライアント JAVASCRIPT SDK](~/tabs/how-to/using-teams-client-sdk.md)には、開発者がコンテンツページを開発する際に役に立つことがある、多くの追加機能が用意されています。

### <a name="deep-links"></a>ディープ リンク

Teams のエンティティへの詳細なリンクを作成できます。 通常、これらは、タブ内のコンテンツと情報に移動するリンクを作成するために使用されます。「 [Microsoft Teams のコンテンツと機能への詳細なリンクを作成する」を](~/concepts/build-and-test/deep-links.md)参照してください。

### <a name="task-modules"></a>タスクモジュール

タスクモジュールは、タブからトリガーできるモーダルのポップアップ表示のようなものです。通常、コンテンツページでは、複数のページを介してユーザーを移動する必要はありません。 その代わりに、タスクモジュールを使用して、追加情報を収集するためのフォームを表示したり、リスト内のアイテムの詳細を表示したり、またはその他の時間についてユーザーに追加情報を提示する必要があります。 タスクモジュール自体は、追加のコンテンツページにすることも、アダプティブカードを使用して完全に作成することもできます。 詳細については、「 [tab でタスクモジュールを使用する](~/task-modules-and-cards/task-modules/task-modules-tabs.md)」を参照してください。

### <a name="valid-domains"></a>有効なドメイン

タブで使用されているすべての URL ドメインがマニフェスト内の配列に含まれていることを確認し `validDomains` ます。 [manifest](~/concepts/build-and-test/apps-package.md) 詳細については、「マニフェストスキーマリファレンス」の「 [Validdomains](~/resources/schema/manifest-schema.md#validdomains) 」を参照してください。 ただし、タブのコア機能は teams 内に存在し、Teams の外部ではないことに注意してください。

## <a name="show-a-native-loading-indicator"></a>ネイティブローディングインジケーターを表示する

[マニフェストスキーマ](../../../resources/schema/manifest-schema.md)v2.0 以降では、web コンテンツが Teams ([タブのコンテンツページ](#integrate-your-code-with-teams)、[構成ページ](configuration-page.md)、[削除ページ](removal-page.md)、[タスクモジュール](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)など) に読み込まれているすべての場所で、[ネイティブの読み込みインジケーター](../../../resources/schema/manifest-schema.md#showloadingindicator)を提供できます。

> [!NOTE]
> アプリマニフェストで指定する場合は、 `"showLoadingIndicator : true` すべてのタブ構成、コンテンツ、および削除ページと、すべての iframe ベースのタスクモジュールは、以下の必須プロトコルに従う必要があります。

1. 読み込みインジケーターを表示するには、 `"showLoadingIndicator": true` マニフェストにを追加します。 
2. にお問い合わせ `microsoftTeams.initialize();` ください。
3. **省略可能**です。 画面に印刷する準備ができていて、アプリケーションのコンテンツの残りの部分を遅延ロードする必要がある場合は、を呼び出して、読み込みインジケーターを手動で非表示にすることができます。`microsoftTeams.appInitialization.notifyAppLoaded();`
4. **必須**。 最後に、 `microsoftTeams.appInitialization.notifySuccess()` アプリが正常に読み込まれたことを Teams に通知する呼び出しを行います。 チームは、必要に応じて、読み込みインジケーターを非表示にします。 `notifySuccess`が30秒以内に呼び出されない場合は、アプリがタイムアウトになり、[再試行] オプションのあるエラー画面が表示されることを前提としています。
5. アプリケーションの読み込みに失敗した場合は、 `microsoftTeams.appInitialization.notifyFailure(reason);` チームにエラーがあることを知らせるための呼び出しを行うことができます。 エラー画面がユーザーに表示されます。

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
