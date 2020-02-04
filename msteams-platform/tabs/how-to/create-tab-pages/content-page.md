---
title: コンテンツページを作成する
author: laujan
description: ''
keywords: teams タブグループチャネルの構成可能な静的
ms.topic: conceptual
ms.author: v-laujan
ms.openlocfilehash: ac85e000c9bdaebf28cb33143a7c82a348d3771e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674875"
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

ページを Teams に表示するには、 [Microsoft Teams の JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest)を含み、ページの読み込み後`microsoftTeams.initialize()`にの呼び出しを含める必要があります。 ページと Teams クライアントが通信する方法は次のとおりです。

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

タブで使用されているすべての URL ドメインが[マニフェスト](~/concepts/build-and-test/apps-package.md)内`validDomains`の配列に含まれていることを確認します。 詳細については、「マニフェストスキーマリファレンス」の「 [Validdomains](~/resources/schema/manifest-schema.md#validdomains) 」を参照してください。 ただし、タブのコア機能は teams 内に存在し、Teams の外部ではないことに注意してください。
