---
author: heath-hamilton
description: 最初の Microsoft Teams アプリ用に [チャネル] タブを作成する方法について説明します。
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
title: Teams の [チャネル] タブを作成する
ms.openlocfilehash: d0846c3af23fd9df6013f989e9f455f711d05a5f
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210255"
---
# <a name="build-a-teams-channel-tab"></a>Teams の [チャネル] タブを作成する

このチュートリアルでは、チームチャネルまたはチャットの全画面コンテンツページである基本 *チャネルタブ*を作成します。 [個人用] タブとは異なり、ユーザーは [チャネル] タブのいくつかの側面を構成できます (たとえば、タブの名前を変更して、チャネルにとって意味がある場合)。

## <a name="before-you-begin"></a>はじめに

開始するには、基本的な実行アプリが必要です。 使用していない場合は、 [ビルドを実行し、Teams 最初のアプリの手順を実行](../build-your-first-app/build-and-run.md)します。 アプリプロジェクトを作成するときは、[ **グループまたはチームチャネル] タブ** のオプションのみを選択します。

## <a name="your-assignment"></a>自分の割り当て

以前は、組織で重要な機能 (help desk、HR など) への連絡方法に関する情報を含む Teams タブが作成されていました。 ただし、タブは個人用の用途に対してのみスコープ設定されているため、各ユーザーはタブをインストールして、それを表示し、導入が予想よりも低くなるようにする必要があります。 つまり、まだ多くのワーカーがヘルプデスクに到達する方法がわからない場合があります。

[チャネル] タブを作成することによって、この情報を見つけやすくすることができます。これにより、アプリのインストールをすべてのユーザーに対して要求する手間が軽減されます。 代わりに、1人のユーザーが、グループ全体の利点を得るために、チャネルまたはチャットにタブをインストールすることができます。

## <a name="what-youll-learn"></a>学習内容

> [!div class="checklist"]
>
> * チャネルタブに関連するアプリマニフェストのプロパティとスキャフォールディングの一部を特定する
> * タブのコンテンツを作成する
> * タブの構成ページのコンテンツを作成する
> * タブを構成およびインストールできるようにする
> * 提案されたタブ名を指定する

## <a name="identify-relevant-app-project-components"></a>関連するアプリプロジェクトコンポーネントを特定する

Teams ツールキットを使用してプロジェクトを作成すると、アプリマニフェストとスキャフォールディングの多くが自動的に設定されます。 [チャネル] タブを作成するための主なコンポーネントについて説明します。

### <a name="app-manifest"></a>アプリマニフェスト

アプリマニフェストの次のスニペットが表示され [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) ます。これには、チャネルタブに関連するプロパティと既定値が含まれています。

```JSON
"configurableTabs": [
    {
        "configurationUrl": "{baseUrl0}/config",
        "canUpdateConfiguration": true,
        "scopes": [
            "team",
            "groupchat"
        ]
    }
],
```

* `configurationUrl`: タブの構成ページのホスト URL (HTTPS である必要があります)。
* `canUpdateConfiguration`: に設定さ `true` れている場合、ユーザーはタブの設定を変更するか、タブの名前を変更するか、チャネルまたはチャットから削除することができます。
* `scopes`: ユーザーがアプリをチャネル ( `team` ) およびチャット () にインストールできるかどうかを指定し `groupchat` ます。 少なくとも1つの値が必要です。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングは、 `TabConfig.js` `src/components` タブの構成ページをレンダリングするために、プロジェクトのディレクトリにあるファイルを提供します (詳細については、すぐに説明します)。

## <a name="create-your-tab-content"></a>タブコンテンツを作成する

ディレクトリでアプリマニフェスト ( `manifest.json` ) を開き `.publish` 、で次のプロパティを設定し [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) ます。タブのコンテンツページが定義されています。

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "My Contacts",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

次のスニペットを、組織に関連する情報でコピーして更新するか、または時間のためにコードをそのように使用します。

```JSX
<div>
  <h1>Important Contacts</h1>
    <ul>
      <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
      <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
      <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
    </ul>
</div>
```

ディレクトリに移動 `src/components` し、を開き `Tab.js` ます。 関数を検索し、その `render()` 中にコンテンツを貼り付け `return()` ます (図を参照)。

```JavaScript
render() {

    let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

    return (
    <div>
      <h1>Important Contacts</h1>
        <ul>
          <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
          <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
          <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
        </ul>
    </div>
    );
}
```

`App.css`どのテーマが使用されていても、電子メールリンクが読みやすくなるように、次のルールを追加します。

```CSS
a {
  color: inherit;
}
```

## <a name="create-your-tab-configuration-page"></a>タブの構成ページを作成する

各 [チャネル] タブには構成ページがあり、アプリをインストールするときに表示される1つ以上のセットアップオプションを持つモーダルです。 既定では、構成ページは、タブがインストールされたときにチャネルまたはチャットに通知するかどうかをユーザーに確認します。

構成ページにコンテンツを追加します。 プロジェクトのディレクトリに移動し、を `src/components` 開いて、その内部にコンテンツを挿入し `TabConfig.js` `return()` ます (図を参照)。

```JavaScript
return (
    <div>
      <h1>Add My Contoso Contacts</h1>
      <div>
        Select <b>Save</b> to add our organization's important contacts to this workspace.
      </div>
    </div>
);
```
 
> [!TIP]
> 少なくとも、ユーザーが初めて理解しているときに、このページにあるアプリについて簡単な情報を提供します。 また、タブの構成ページに共通のカスタム構成オプションまたは [認証ワークフロー](../tabs/how-to/authentication/auth-aad-sso.md)を含めることもできます。

## <a name="allow-the-tab-to-be-configured-and-installed"></a>タブを構成およびインストールできるようにする

ユーザーが [チャネル] タブを正しく構成してインストールするには、 [最初のアプリを作成し](../build-your-first-app/build-and-run.md) て構成ページコンポーネントに対して実行するときに設定するホスト URL を追加する必要があります。

に移動 `TabConfig.js` し、を見つけ `microsoftTeams.settings.setSettings` ます。 の場合は `"contentUrl"` 、 `localhost:3000` URL の部分を、タブの内容をホストしているドメインに置き換えます (図を見てください)。

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

また、があることを確認してください `microsoftTeams.settings.setValidityState(true);` 。 既定では、がに設定されている場合 `false` 、[構成] ページの [ **保存** ] ボタンは無効になっています。

## <a name="provide-a-suggested-tab-name"></a>提案されたタブ名を指定する

個人用に使用するタブをインストールすると、表示名は、 `name` `staticTabs` アプリマニフェストの一部のプロパティ (たとえば、 **[連絡先**]) になります。 [チャネル] タブをインストールすると、既定ではアプリケーション名が表示されます (たとえば、 **最初のアプリ**)。

これは、アプリの呼び出し方法によっては適切な場合もありますが、グループコラボレーションのコンテキスト (たとえば、 **チーム連絡先**) にとってわかりやすい名前を指定することをお勧めします。

で `TabConfig.js` 、に戻り `microsoftTeams.settings.setSettings` ます。 `suggestedDisplayName`既定で表示するタブ名を持つプロパティを追加します (表示されています)。 指定した名前を使用するか、独自の名前を作成します。 マニフェストでは、必要に応じてユーザーが名前を変更できるようにすることを忘れないでください。

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="view-the-channel-tab"></a>[チャネル] タブを表示する

チャネルタブの構成とコンテンツページを表示するには、チャネルまたはチャットにインストールする必要があります。

1. Teams クライアントで、[ **アプリ**] を選択します。
1. [ **カスタムアプリのアップロード** ] を選択し、アプリを選択し `Development.zip` ます。
1. [ **チームに追加する** ] または [ **チャットに追加** する] を選択し、テストに使用できるチャネルまたはチャットを探します。
1. [ **タブの設定]** を選択します。[構成] ページが表示されます。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="[チャネル] タブの構成ページのスクリーンショット。":::
1. [ **保存** ] を選択してタブを構成します。コンテンツが表示されます。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツビューがある [チャネル] タブのスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

おめでとうございます! [チャネル] タブを備えた Teams アプリを使用すると、チャンネルやチャットに役立つコンテンツを表示できます。

## <a name="learn-more"></a>詳細情報

* [認証タブのユーザーに SSO を使用](../tabs/how-to/authentication/auth-aad-sso.md)する: 承認されたユーザーのみにタブを表示する場合は、Azure Active DIRECTORY (AD) を使用してシングルサインオン (SSO) を設定します。
* [既存の web アプリまたは web ページからコンテンツを埋め込む](../tabs/how-to/add-tab.md#tab-requirements): [個人用] タブの新しいコンテンツを作成する方法を示しましたが、外部 URL からコンテンツを読み込むこともできます。
* [タブに対してシームレスな環境を作成する](../tabs/design/tabs.md): Teams タブの設計に関する推奨ガイドラインを参照してください。
* [モバイル用のタブの作成](../tabs/design/tabs-mobile.md): 電話とタブレットのタブを開発する方法について理解します。
* [ツールキットなしでタブを作成する](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>次のレッスン

グループ作業用のタブを作成する方法を理解していること。 別の種類の Teams アプリを作成しようとしていますか?

> [!div class="nextstepaction"]
> [Bot を構築する](../build-your-first-app/build-bot.md)
