---
title: 「はじめに」-「チャネルとグループの作成」タブ
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams のチャネルとグループタブをすばやく作成できます。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: f890754cdf4ca43f39c25e3ba24fcf47b08c5a9f
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452856"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>Microsoft Teams の [チャネルとグループの作成] タブ

このチュートリアルでは、チームチャネルまたはチャットの全画面ページである基本 *チャネルタブ* ( *グループタブ*とも呼ばれます) を作成します。 [個人用] タブとは異なり、ユーザーはこの種類のタブのいくつかの側面を構成できます (たとえば、タブの名前を変更して、チャネルにとって意味がある場合)。

## <a name="your-assignment"></a>自分の割り当て

以前は、組織で重要な機能 (help desk、HR など) への連絡方法に関する情報を含む Teams タブが作成されていました。 ただし、タブは個人用の用途に対してのみスコープ設定されているため、各ユーザーはタブをインストールして、それを表示し、導入が予想よりも低くなるようにする必要があります。 つまり、まだ多くのワーカーがヘルプデスクに到達する方法がわからない場合があります。

[チャネル] タブを作成することによって、この情報を見つけやすくすることができます。これにより、アプリのインストールをすべてのユーザーに対して要求する手間が軽減されます。 代わりに、1人のユーザーが、グループ全体の利点を得るために、チャネルまたはチャットにタブをインストールすることができます。

## <a name="what-youll-learn"></a>学習内容

> [!div class="checklist"]
>
> * Microsoft Teams Toolkit for Visual Studio Code を使用してアプリプロジェクトを作成する
> * チャネルおよびグループのタブに関連するアプリマニフェストのプロパティとスキャフォールディングの一部を特定する
> * アプリをローカルでホストする
> * タブのコンテンツを作成する
> * タブの構成ページのコンテンツを作成する
> * タブを構成およびインストールできるようにする
> * 提案されたタブ名を指定する

## <a name="1-create-your-app-project"></a>1. アプリプロジェクトを作成します。

Microsoft Teams Toolkit は、"Hello, World!" と表示される基本的な構成ページやコンテンツページなど、チャネルおよびグループのタブに関連するアプリのマニフェストとスキャフォールディングを設定するのに役立ちます。 メッセージ。

> [!TIP]
> 以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)
1. [ **機能の追加** ] 画面で、[ **タブ** 、 **グループ、またはチームチャネル] タブ**を選択します。
1. 画面の下部にある [ **完了** ] を選択して、プロジェクトを構成します。  

## <a name="2-identify-relevant-app-project-components"></a>2. 関連するアプリプロジェクトコンポーネントを特定する

Teams ツールキットを使用してプロジェクトを作成すると、アプリマニフェストとスキャフォールディングの多くが自動的に設定されます。 [チャネルとグループ] タブを構築するための主なコンポーネントについて見てみましょう。

### <a name="app-manifest"></a>アプリマニフェスト

アプリマニフェストの次のスニペットは [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) 、[チャネル] タブおよび [グループ] タブに関連するプロパティと既定値を含みます。

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

## <a name="3-run-your-app"></a>3. アプリを実行する

時間の経過とともに、アプリをローカルでビルドして実行します。

1. ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。
1. `npm start` を実行します。

完了すると、**コンパイルに成功**しました。 ターミナルのメッセージ。

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a>4. アプリへのセキュリティで保護されたトンネルをセットアップする

テストを目的として、ローカル web サーバー (ポート 3000) 上でタブをホストしてみましょう。

1. ターミナルで、を実行 `ngrok http 3000` します。
1. 提供されている HTTPS URL をコピーします。
1. ディレクトリで `.publish` 、を開き `Development.env` ます。
1. 値を `baseUrl0` コピーした URL に置き換えます。 (たとえば、 `baseUrl0=http://localhost:3000` をに変更 `baseUrl0=https://85528b2b3ca5.ngrok.io` します)。

アプリのマニフェストは、タブをホストしている場所を指しています。

## <a name="5-customize-your-tab-content-page"></a>5. タブのコンテンツページをカスタマイズする

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

## <a name="6-create-your-tab-configuration-page"></a>6. [タブの構成] ページを作成する

チャネルまたはチャットのすべてのタブには構成ページがあります。このページには、ユーザーがアプリをインストールするときに表示されるセットアップオプションが1つ以上あるモーダルがあります。 既定では、構成ページは、タブがインストールされたときにチャネルまたはチャットに通知するかどうかをユーザーに確認します。

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

## <a name="7-allow-the-tab-to-be-configured-and-installed"></a>7. タブを構成してインストールできるようにする

ユーザーがタブを正しく構成およびインストールするには、構成ページコンポーネントに設定した、 [セキュリティで保護さ](#4-set-up-a-secure-tunnel-to-your-app) れたホストの URL を追加する必要があります。

に移動 `TabConfig.js` し、を見つけ `microsoftTeams.settings.setSettings` ます。 の場合は `"contentUrl"` 、 `localhost:3000` URL の部分を、タブの内容をホストしているドメインに置き換えます (図を見てください)。

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

また、があることを確認してください `microsoftTeams.settings.setValidityState(true);` 。 既定では、がに設定されている場合 `false` 、[構成] ページの [ **保存** ] ボタンは無効になっています。

## <a name="8-provide-a-suggested-tab-name"></a>8. 提案されたタブ名を指定する

個人用に使用するタブをインストールすると、表示名は、 `name` `staticTabs` アプリマニフェストの一部のプロパティ (たとえば、 **[連絡先**]) になります。 [チャネル] タブをインストールすると、既定ではアプリケーション名が表示されます (たとえば、 **最初のアプリ**)。

これは、アプリの呼び出し方法によっては適切な場合もありますが、グループコラボレーションのコンテキスト (たとえば、 **チーム連絡先**) にとってわかりやすい名前を指定することをお勧めします。

で `TabConfig.js` 、に戻り `microsoftTeams.settings.setSettings` ます。 `suggestedDisplayName`既定で表示するタブ名を持つプロパティを追加します (表示されています)。 指定した名前を使用するか、独自の名前を作成します。 マニフェストでは、必要に応じてユーザーが名前を変更できるようにすることを忘れないでください。

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="9-view-the-tab"></a>9. タブを表示する

タブの構成とコンテンツページを表示するには、チャネルまたはチャットにインストールする必要があります。

1. Teams クライアントで、[ **アプリ**] を選択します。
1. [ **カスタムアプリのアップロード** ] を選択し、アプリを選択し `Development.zip` ます。
1. [ **チームに追加する** ] または [ **チャットに追加** する] を選択し、テストに使用できるチャネルまたはチャットを探します。
1. [ **タブの設定]** を選択します。[構成] ページが表示されます。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="[チャネル] タブの構成ページのスクリーンショット。":::
1. [ **保存** ] を選択してタブを構成します。コンテンツが表示されます。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="[チャネル] タブの構成ページのスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

おめでとうございます! Teams アプリには、チャネルとチャットに役立つコンテンツを表示するためのタブがあります。

## <a name="learn-more"></a>詳細情報

* [認証タブのユーザーに SSO を使用](../tabs/how-to/authentication/auth-aad-sso.md)する: 承認されたユーザーのみにタブを表示する場合は、Azure Active DIRECTORY (AD) を使用してシングルサインオン (SSO) を設定します。
* [既存の web アプリまたは web ページからコンテンツを埋め込む](../tabs/how-to/add-tab.md#tab-requirements): [個人用] タブの新しいコンテンツを作成する方法を示しましたが、外部 URL からコンテンツを読み込むこともできます。
* [タブに対してシームレスな環境を作成する](../tabs/design/tabs.md): Teams タブの設計に関する推奨ガイドラインを参照してください。
* [モバイル用のタブの作成](../tabs/design/tabs-mobile.md): 電話とタブレットのタブを開発する方法について理解します。
* [ツールキットなしでタブを作成する](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>次のレッスン

グループ作業用のタブを作成する方法を理解していること。 別の種類の Teams アプリを作成しようとしていますか?

> [!div class="nextstepaction"]
> [Bot を作成する](../build-your-first-app/build-bot.md)
