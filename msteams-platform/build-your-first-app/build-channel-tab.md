---
title: 「はじめに」-「チャネルとグループの作成」タブ
author: heath-hamilton
description: Microsoft Teams ツールキットを使用して、Microsoft Teams のチャネルとグループタブをすばやく作成できます。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: bb87d34974469057287cf63725e7722125c57c34
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605246"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>Microsoft Teams の [チャネルとグループの作成] タブ

このチュートリアルでは、チームチャネルまたはチャットの全画面ページである基本 *チャネルタブ* ( *グループタブ* とも呼ばれます) を作成します。 [個人用] タブとは異なり、ユーザーはこの種類のタブのいくつかの側面を構成できます (たとえば、タブの名前を変更して、チャネルにとって意味がある場合)。

## <a name="your-assignment"></a>自分の割り当て

以前は、タブを使用して重要な連絡先情報 (ヘルプデスク、人事など) を表示する Teams アプリを作成しています。 ただし、[個人用] タブなので、各ユーザーは、そのタブをインストールして表示する必要があり、導入が予想よりも低いことを示します。 つまり、まだ多くのワーカーがヘルプデスクに到達する方法がわからない場合があります。

[チャネル] タブを作成することによって、この情報を見つけやすくすることができます。これにより、アプリのインストールをすべてのユーザーに対して要求する手間が軽減されます。 代わりに、1人のユーザーがチャネルまたはチャットにタブを追加して、グループ全体の利点を得ることができます。

## <a name="what-youll-learn"></a>学習内容

> [!div class="checklist"]
>
> * Microsoft Teams Toolkit for Visual Studio Code を使用してアプリプロジェクトを作成する
> * チャネルおよびグループのタブに関連するアプリの構成とスキャフォールディングの一部を特定する
> * タブのコンテンツを作成する
> * タブの構成ページのコンテンツを作成する
> * 提案されたタブ名を指定する
> * アプリをローカルでビルドして実行する
> * テストのために Teams でアプリをサイドロードする

## <a name="before-you-begin"></a>開始する前に

まだお持ちでない場合は、 [Teams 開発の前提条件を理解し、インストール](build-first-app-overview.md#get-prerequisites)してください。

## <a name="1-create-your-app-project"></a>1. アプリプロジェクトを作成します。

Microsoft Teams ツールキットは、アプリを構成し、[チャネル] タブおよび [グループ] タブに関連するスキャフォールディングをセットアップするのに役立ちます。これには、基本的な構成ページと、"Hello, World!" を表示するコンテンツページが含まれます。 メッセージ。

> [!TIP]
> 以前に Teams アプリプロジェクトを作成していない場合は、 [以下の手順](../build-your-first-app/build-and-run.md) に従って、プロジェクトについて詳しく説明することをお勧めします。

1. Visual Studio Code で、左側のアクティビティバーにある [ **Microsoft teams** ] を選択 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: し、[ **新しい teams アプリの作成**] を選択します。
1. メッセージが表示されたら、Microsoft 365 開発アカウントでサインインします。
1. [ **機能の追加** ] 画面で、[ **タブ]** 、[ **次へ**] の順に選択します。
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前であり、ローカルコンピューター上のアプリプロジェクトディレクトリの名前でもあります。)
1. [ **個人用] タブ** および [ **グループ] または [チームチャネル] タブ** のオプションを確認します。 (両方の種類のタブが必要な理由については、すぐに説明します)。
1. 画面の下部にある [ **完了** ] を選択して、プロジェクトを構成します。  

## <a name="2-identify-relevant-app-project-components"></a>2. 関連するアプリプロジェクトコンポーネントを特定する

Teams ツールキットを使用してプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。 [チャネルとグループ] タブを構築するための主なコンポーネントについて見てみましょう。

### <a name="app-configurations"></a>アプリの構成

アプリの構成は、ツールキットに含まれる App Studio を使用して表示および更新できます。

セットアップ時に、ツールキットは、最初はチャネルとグループのタブの2つの重要なコンポーネントを構成しました。

* **構成ページ**: チャネルまたはチャットにタブを追加するためのモーダル。 (アプリ Studio では、[ **チーム] タブ > タブ** に移動して、このページを見つけることができます)。
* **コンテンツページ**: プライマリコンテンツを表示する場所。 (アプリ Studio では、 **タブ > [個人用] タブ** に移動することで、このページを見つけることができます)。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングは、Teams で個人用タブを表示するためのコンポーネントを提供します。 多くの作業を行うことができますが、現時点では、次の点を重視するだけで十分です。

* プロジェクトのディレクトリにある2つのファイル `src/components` :
  * `Tab.js` タブのコンテンツページをレンダリングします。
  * `TabConfig.js` タブの構成ページをレンダリングします。
* Microsoft Teams JavaScript クライアント SDK。これは、プロジェクトのフロントエンドコンポーネントに事前に読み込まれています。

## <a name="3-customize-your-tab-content-page"></a>3. タブのコンテンツページをカスタマイズする

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

`App.css` `src/components` どのテーマが使用されていても、電子メールリンクが読みやすくなるように、次のルールを (にも) 追加します。

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a>4. タブの構成ページをカスタマイズする

チャネルまたはチャットのすべてのタブには構成ページがあります。このページには、ユーザーがアプリを追加するときに表示されるセットアップオプションが1つ以上あるモーダルがあります。 既定では、構成ページは、タブがインストールされたときにチャネルまたはチャットに通知するかどうかをユーザーに確認します。

カスタムコンテンツを構成ページに追加します。 プロジェクトのディレクトリに移動し、 `src/components` `TabConfig.js` プレースホルダーのコンテンツを `return()` (次の例に示すように) 表示して、更新します。

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

## <a name="5-provide-a-suggested-tab-name"></a>5. 提案されたタブ名を指定する

チャネルまたはグループタブを追加すると、既定ではアプリケーション名が表示されます (たとえば、 **最初のアプリ**)。

これは、アプリの呼び出し方法によっては適切な場合もありますが、グループコラボレーションのコンテキスト (たとえば、 **チーム連絡先**) にとってわかりやすい名前を指定することをお勧めします。

で `TabConfig.js` 、に移動 `microsoftTeams.settings.setSettings` します。 `suggestedDisplayName`既定で表示するタブ名を持つプロパティを追加します (表示されています)。 指定した名前を使用するか、独自の名前を作成します。 (既定では、ユーザーは必要に応じて名前を変更できます。)

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a>6. アプリをビルドして実行します。

時間の経過とともに、アプリをローカルでビルドして実行します。

(この情報は、ツールキットでも利用でき `README` ます。)

1. ターミナルで、アプリプロジェクトのルートディレクトリに移動し、を実行 `npm install` します。
1. `npm start` を実行します。

完了すると、**コンパイルに成功** しました。 ターミナルのメッセージ。 アプリが実行されている `https://localhost:3000` 。

## <a name="7-sideload-your-app-in-teams"></a>7. Teams でアプリをサイドロードする

アプリは Teams でテストする準備ができています。 これを行うには、アプリのサイドロードを許可するアカウントが必要です。 (あるかどうかがわからない場合は、 [Teams 開発アカウント](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)の取得についてを参照してください)。

1. Visual Studio Code で、 **F5** キーを押して Teams web クライアントを起動します。
1. Teams でアプリのコンテンツを表示するには、アプリが実行されている場所 () を信頼するように指定し `localhost` ます。
   1. **F5** キーを押した後に開いた同じブラウザーウィンドウ (既定では Google Chrome) で新しいタブを開きます。
   1. に移動 `https://localhost:3000/tab` して、ページに進みます。
1. Teams に戻ります。 モーダルで、[ **チームに追加する** ] または [ **チャットに追加** する] を選択し、テストに使用できるチャネルまたはチャットを探します。
1. [ **タブの設定]** を選択します。構成ページがモーダルで表示されます。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="[チャネル] タブの構成ページのスクリーンショット。":::
1. [ **保存** ] を選択してタブを構成します。コンテンツページが表示されます。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツビューがある [チャネル] タブのスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

おめでとうございます! Teams アプリには、チャネルとチャットに役立つコンテンツを表示するためのタブがあります。

## <a name="learn-more"></a>詳細情報

* [認証タブのユーザーに SSO を使用](../tabs/how-to/authentication/auth-aad-sso.md)する: 承認されたユーザーのみにタブを表示する場合は、Azure Active DIRECTORY (AD) を使用してシングルサインオン (SSO) を設定します。
* [既存の web アプリまたは web ページからコンテンツを埋め込む](../tabs/how-to/add-tab.md#tab-requirements): [個人用] タブの新しいコンテンツを作成する方法を示しましたが、外部 URL からコンテンツを読み込むこともできます。
* [タブに対してシームレスな環境を作成する](../tabs/design/tabs.md): Teams タブの設計に関する推奨ガイドラインを参照してください。
* [モバイル用のタブの作成](../tabs/design/tabs-mobile.md): 電話とタブレットのタブを開発する方法について理解します。
* [Microsoft Graph API で Teams データを利用する](https://docs.microsoft.com/graph/teams-concept-overview)
* [ツールキットなしでタブを作成する](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>次のレッスン

グループ作業用のタブを作成する方法を理解していること。 別の種類の Teams アプリを作成しようとしていますか?

> [!div class="nextstepaction"]
> [Bot を作成する](../build-your-first-app/build-bot.md)
