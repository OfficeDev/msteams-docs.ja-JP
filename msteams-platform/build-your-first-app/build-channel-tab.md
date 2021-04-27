---
title: '[スタート] - [チャネルとグループ] タブを作成する'
author: heath-hamilton
description: Microsoft Teams チャネルとグループ タブを Microsoft Teams チャネルとグループ タブを使用してすばやく作成Toolkit。
ms.author: lajanuar
localization_priority: Normal
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: aadab4b6826b026eadd5ed564b6e5de5c29b4b1d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020878"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>Microsoft Teams のチャネルとグループ タブを作成する

このチュートリアルでは、チーム チャネルまたはチャットのフルスクリーン ページである基本的なチャネルタブ *(グループ* タブとも呼ばれる) を作成します。 個人用タブとは異なり、ユーザーは、この種のタブのいくつかの側面を構成できます (たとえば、タブの名前を変更して、チャネルにとって意味のあるものにします)。

## <a name="your-assignment"></a>割り当て

少し前に、組織はタブを使用して重要な連絡先情報 (ヘルプ デスク、人事など) を表示する Teams アプリを作成しました。 ただし、個人用タブだから、各ユーザーがタブをインストールして表示し、導入が予想より低くなります。 つまり、ヘルプ デスクに到達する方法をまだ知らないワーカーが多すぎます。

チャネル タブを作成すると、この情報を見つけやすくすることができます。これにより、すべてのユーザーにアプリのインストールを要求する負担が軽減されます。 代わりに、1 人のユーザーがグループ全体の利益のために、チャネルまたはチャットにタブを追加できます。

## <a name="what-youll-learn"></a>学習する情報

> [!div class="checklist"]
>
> * Microsoft Teams を使用してアプリ プロジェクトを作成ToolkitコードVisual Studioする
> * チャネル タブに関連するアプリ構成とスキャフォールディングの一部を特定する
> * タブ コンテンツの作成
> * タブの構成ページのコンテンツを作成する
> * 推奨されるタブ名を指定する
> * アプリをローカルでビルドして実行する
> * テスト用に Teams でアプリをサイドロードする

## <a name="before-you-begin"></a>はじめに

まだインストールしていない場合は、Teams 開発の [前提条件を理解してインストールしてください](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

Microsoft Teams Toolkitは、アプリを構成し、チャネルタブとグループ タブに関連するスキャフォールディングを設定するのに役立ちます。基本的な構成ページや、"Hello, World! メッセージ。

> [!TIP]
> 以前に Teams アプリ プロジェクトを作成したことがない場合は、プロジェクトの詳細を[](../build-your-first-app/build-and-run.md)説明する手順に従うのが役に立つ場合があります。

1. Visual Studio Code で、左側の [アクティビティ バー] で [**Microsoft Teams**] :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: を選択し、[**新しい Teams アプリを作成する**] を選択します。
1. メッセージが表示されたら、Microsoft 365 開発アカウントを使用してサインインします。
1. [**機能の追加**] 画面で、[**タブ**] を選択し、[**次へ**] を選択します。
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前であり、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。[グループ **] または [Teams チャネル] タブを選択します**。
1. 画面 **の下部** にある [完了] を選択して、プロジェクトを構成します。  

## <a name="2-identify-relevant-app-project-components"></a>2. 関連するアプリ プロジェクト コンポーネントを特定する

ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。 チャネル タブを作成する主要なコンポーネントを見てみ取ってみろ。

### <a name="app-configurations"></a>アプリの構成

ツールキットで、App Studio に **移動して** 、アプリ構成を表示および更新します。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングは、Teams でチャネル タブをレンダリングするコンポーネントを提供します。 多くの作業が可能ですが、今のところ、次の作業に集中する必要があります。

* プロジェクトのディレクトリに 2 `src/components` つのファイルがあります。
  * `Tab.js` タブのコンテンツ ページをレンダリングします。
  * `TabConfig.js` タブの構成ページをレンダリングします。
* プロジェクトのフロントエンド コンポーネントに事前に読み込まれた Microsoft Teams JavaScript クライアント SDK。

## <a name="3-customize-your-tab-content-page"></a>3. タブ コンテンツ ページをカスタマイズする

組織に関連する情報を含む次のスニペットをコピーして更新するか、時間の間はコードを使用します。

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

ディレクトリに移動 `src/components` して開きます `Tab.js` 。 関数を見 `render()` つけて、コンテンツを (図のように) `return()` 内部に貼り付けます。

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

使用するテーマに関係なく、電子メール リンクを読みやすくするために、次のルールを (に含む `App.css` `src/components` ) に追加します。

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a>4. タブ構成ページをカスタマイズする

チャネルまたはチャットのすべてのタブには構成ページがあります。モーダルで、ユーザーがアプリを追加するときに少なくとも 1 つのセットアップ オプションが表示されます。 既定では、構成ページは、タブがインストールされているときにチャネルまたはチャットに通知する必要がある場合に、ユーザーに通知を求めるメッセージを表示します。

構成ページにカスタム コンテンツを追加します。 プロジェクトのディレクトリに移動し、開き、内部のプレースホルダー コンテンツ `src/components` `TabConfig.js` を更新します (次 `return()` の例に示すように)。

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
> 少なくとも、このページでアプリに関する簡単な情報は、ユーザーが初めて学習する場合があります。 カスタム構成オプションや、タブ構成ページで一般的 [な](../tabs/how-to/authentication/auth-aad-sso.md)認証ワークフローを含めすることもできます。

## <a name="5-provide-a-suggested-tab-name"></a>5. 推奨されるタブ名を指定する

チャネル タブを追加すると、既定でアプリ名が表示されます (ファースト アプリ **など**)。

これは、アプリの呼び出し内容に応じて問題ありませんが、グループの共同作業 (チーム連絡先など) のコンテキストで意味のある名前を指定することもできます **。**

1. に `TabConfig.js` 移動します `microsoftTeams.settings.setSettings` 。
2. 既定で `suggestedDisplayName` 表示するタブ名を含むプロパティを追加します。 
3. 次の例に示す名前を使用するか、名前を入力します。 (既定では、ユーザーは名前を変更できます)。

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a>6. アプリをビルドして実行する

時間に関して、アプリをローカルでビルドして実行します。

(この情報はツールキットでも利用 `README` できます。)

1. ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、`npm install` を実行します。
1. `npm start` を実行します。

完了すると、[**正常にコンパイルされました**] と表示されます。 ターミナルのメッセージ。 お使いのアプリは `https://localhost:3000` で動作しています。

## <a name="7-sideload-your-app-in-teams"></a>7. Teams でアプリをサイドロードする

お使いのアプリは Teams でテストする準備ができています。 これを行うには、アプリのサイドローディングを許可するアカウントが必要です。 (確信が持てない場合は、Teams 開発アカウントを取得する方法 [について説明します](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。)

1. [Visual Studioコード] で **、F5** キーを押して Teams Web クライアントを起動します。
1. アプリ コンテンツを Teams で表示するには、信頼できるアプリを実行する場所 (`localhost`) を指定します。
   1. **F5** を押した後に開いたのと同じブラウザー ウィンドウ (既定では Google Chrome) で新しいタブを開きます。
   1. `https://localhost:3000/tab` に進み、ページを進めます。
1. Teams に戻ります。 モーダルで、[チームに追加 **]** または[チャットに追加] を選択し、テストに使用できるチャネルまたはチャットを探します。
1. [タブ **の設定] を選択します**。構成ページはモーダルで表示されます。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="チャネル タブ構成ページのスクリーンショット。":::
1. [保存 **] を** 選択してタブを構成します。コンテンツ ページが表示されます。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツ ビューを含むチャネル タブのスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

お疲れさまでした。 チャネルやチャットに便利なコンテンツを表示するためのタブを含む Teams アプリがあります。

## <a name="learn-more"></a>詳細情報

* シームレスな [エクスペリエンスを作成するには、](../tabs/design/tabs.md) 設計ガイドラインに従い、実稼働対応 [の UI](../concepts/design/design-teams-app-ui-templates.md) テンプレートを使用してビルドします。
* タブ [のモバイルに関する考慮事項](../tabs/design/tabs-mobile.md) について説明します。
* [タブに SSO 認証を追加します](../tabs/how-to/authentication/auth-aad-sso.md)。
* Microsoft Graph で Teams データ [を利用する](https://docs.microsoft.com/graph/teams-concept-overview)。
* [ツールキットを使用せずにタブを作成する](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a>次のレッスン

コラボレーション用のタブを作成する方法を知っています。 別の種類の Teams アプリの構築を試みませんか?

> [!div class="nextstepaction"]
> [Bot を作成する](../build-your-first-app/build-bot.md)
