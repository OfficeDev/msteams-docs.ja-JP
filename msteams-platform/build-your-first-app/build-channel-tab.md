---
title: 開始する - チャネルとグループ タブを作成する
author: heath-hamilton
description: Microsoft Teams を使用して、Microsoft Teams チャネルとグループ タブをすばやく作成Toolkit。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 2ad0474859118f302a39e823f7669dc54061d525
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795455"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>Microsoft Teams のチャネルとグループ タブを作成する

このチュートリアルでは、基本的なチャネル タブ *(グループ* タブとも呼ばれる) を作成します。これは、チーム チャネルまたはチャットの全画面ページです。 個人用タブとは異なり、ユーザーは、この種のタブの一部を構成できます (たとえば、チャネルにとって意味のある名前に変更します)。

## <a name="your-assignment"></a>割り当て

少し前に、組織はタブを使用して重要な連絡先情報 (ヘルプ デスク、人事など) を表示する Teams アプリを作成しました。 ただし、個人用タブの場合は、各ユーザーがタブをインストールして表示する必要があります。また、導入が予想より低くなります。 言い換えると、多すぎるワーカーは、ヘルプ デスクにアクセスする方法をまだ知りません。

チャネル タブを作成すると、この情報を見つけやすくすることができます。これにより、すべてのユーザーがアプリをインストールする必要が生じやすくなります。 代わりに、1 人のユーザーがチャネルまたはチャットにタブを追加して、グループ全体を利用できます。

## <a name="what-youll-learn"></a>学習する情報

> [!div class="checklist"]
>
> * Microsoft Teams Toolkit for Visual Studio コードを使用してアプリ プロジェクトをVisual Studioする
> * チャネル タブに関連するアプリ構成とスキャフォールディングの一部を特定する
> * タブ コンテンツを作成する
> * タブの構成ページのコンテンツを作成する
> * 推奨されるタブ名を指定する
> * アプリをローカルでビルドして実行する
> * テスト用に Teams でアプリをサイドロードする

## <a name="before-you-begin"></a>はじめに

まだ理解していない場合は、Teams 開発の前提条件 [を理解してインストールしてください](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. アプリ プロジェクトを作成する

Microsoft Teams Toolkit は、アプリを構成し、基本的な構成ページや "Hello, World!" を表示するコンテンツ ページなど、チャネルとグループのタブに関連するスキャフォールディングを設定するのに役立ちます。 メッセージ。

> [!TIP]
> Teams アプリ プロジェクトをまだ作成していない場合は、プロジェクトについて詳しく説明する次[](../build-your-first-app/build-and-run.md)の手順に従うのが役に立つ場合があります。

1. [Visual Studioコード] で、左側のアクティビティ バーで **Microsoft Teams** を選択し、[新しい Teams アプリの作成 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: ] **を選択します**。
1. ダイアログが表示されたら、Microsoft 365 開発アカウントでサインインします。
1. [機能 **の追加] 画面で、[Tab]** を選択し **、[次へ** ] を **選択します**。
1. Teams アプリの名前を入力します。 (これは、アプリの既定の名前と、ローカル コンピューター上のアプリ プロジェクト ディレクトリの名前です)。[グループ **] または [Teams] チャネル タブを選択します**。
1. 画面 **の** 下部にある [完了] を選択して、プロジェクトを構成します。  

## <a name="2-identify-relevant-app-project-components"></a>2. 関連するアプリ プロジェクト コンポーネントを特定する

ツールキットを使ってプロジェクトを作成すると、アプリの構成とスキャフォールディングの多くが自動的に設定されます。 チャネル タブを構築する主なコンポーネントを見てみしましょう。

### <a name="app-configurations"></a>アプリの構成

ツールキットで **、App Studio に移動して** 、アプリの構成を表示および更新します。

### <a name="app-scaffolding"></a>アプリのスキャフォールディング

アプリのスキャフォールディングは、Teams でチャネル タブをレンダリングするコンポーネントを提供します。 作業できる作業は多くあるのですが、今のところは次の作業に集中する必要があります。

* プロジェクトのディレクトリにある 2 `src/components` つのファイル:
  * `Tab.js` タブのコンテンツ ページをレンダリングします。
  * `TabConfig.js` タブの構成ページをレンダリングします。
* Microsoft Teams JavaScript クライアント SDK。プロジェクトのフロントエンド コンポーネントに事前に読み込まれます。

## <a name="3-customize-your-tab-content-page"></a>3. タブ コンテンツ ページをカスタマイズする

組織に関連する情報を使用して次のスニペットをコピーして更新するか、時間の間、コードを使用します。

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

ディレクトリに移動 `src/components` して開きます `Tab.js` 。 関数を見 `render()` つけて、コンテンツを内部 `return()` に貼り付けます (図を参照)。

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

使用するテーマに関係なく、電子メール リンクが読みやすくするために、次のルールを (同じ場所に `App.css` `src/components` ) 追加します。

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a>4. タブ構成ページをカスタマイズする

チャネルまたはチャット内のすべてのタブには構成ページがあります。モーダルで、ユーザーがアプリを追加するときに少なくとも 1 つのセットアップ オプションが表示されます。 既定では、構成ページは、タブのインストール時にチャネルまたはチャットに通知する必要がある場合にユーザーに確認を求めるメッセージを表示します。

構成ページにカスタム コンテンツを追加します。 プロジェクトのディレクトリに移動し、内部のプレースホルダー コンテンツを開いて更新 `src/components` `TabConfig.js` します `return()` (次の例を参照)。

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
> 少なくとも、このページでアプリに関する簡単な情報を提供してください。これは、ユーザーが初めて学習する可能性があります。 また、カスタム構成オプションや、 [タブ構成ページ](../tabs/how-to/authentication/auth-aad-sso.md)で一般的な認証ワークフローを含めすることもできます。

## <a name="5-provide-a-suggested-tab-name"></a>5. 推奨されるタブ名を指定する

チャネル タブを追加すると、既定でアプリ名 (たとえば、最初のアプリ) **が表示されます**。

これは、アプリの呼び出しによって問題ありませんが、グループコラボレーションのコンテキスト (チーム連絡先など) で意味のある名前を付け加える必要がある場合 **があります**。

1. In `TabConfig.js` に移動します `microsoftTeams.settings.setSettings` 。
2. 既定で `suggestedDisplayName` 表示するタブ名を持つプロパティを追加します。 
3. 次の例に示す名前を使用するか、名前を入力します。 (既定では、ユーザーは名前を変更できます)。

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a>6. アプリをビルドして実行する

時間の問題として、アプリをローカルでビルドして実行します。

(この情報はツールキットでも利用 `README` できます)。

1. ターミナルで、アプリ プロジェクトのルート ディレクトリに移動し、実行します `npm install` 。
1. `npm start` を実行します。

完了すると、コンパイルに **成功します。** メッセージが表示されます。 アプリが実行されています `https://localhost:3000` 。

## <a name="7-sideload-your-app-in-teams"></a>7. Teams でアプリをサイドロードする

アプリは Teams でテストする準備が整っています。 これを行うには、アプリのサイドローディングを許可するアカウントが必要です。 (それが確実でない場合は、Teams 開発アカウントを取得する方法 [について説明します](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account))。

1. コードVisual Studio **F5** キーを押して、Teams Web クライアントを起動します。
1. Teams でアプリのコンテンツを表示するには、アプリが実行されている場所 ( `localhost` ) が信頼できる場所を指定します。
   1. F5 キーを押した後に開いた同じブラウザー ウィンドウ (Google Chrome 既定) で新しいタブ **を開きます**。
   1. ページに `https://localhost:3000/tab` 移動し、ページに進みます。
1. Teams に戻る。 モーダルで **、[チームに** 追加] または[チャットに追加] を選択し、テストに使用できるチャネルまたはチャットを探します。
1. [タブ **の設定] を選択します**。構成ページはモーダルで表示されます。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="チャネル タブ構成ページのスクリーンショット。":::
1. [保存 **] を** 選択してタブを構成します。コンテンツ ページが表示されます。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="静的コンテンツ ビューを含むチャネル タブのスクリーンショット。":::

## <a name="well-done"></a>よくやりましたね

おめでとうございます! チャネルやチャットに便利なコンテンツを表示するためのタブを含む Teams アプリがあります。

## <a name="learn-more"></a>詳細情報

* [SSO を使用して](../tabs/how-to/authentication/auth-aad-sso.md)タブ ユーザーを認証する : 承認されたユーザーにのみタブを表示する場合は、Azure Active Directory (AD) を使用してシングル サインオン (SSO) を設定します。
* [既存の Web アプリまたは Web](../tabs/how-to/add-tab.md#tab-requirements)ページからコンテンツを埋め込む : タブの新しいコンテンツを作成する方法を説明しましたが、外部 URL からコンテンツを読み込む方法も示しました。
* [シームレスなタブ エクスペリエンスを作成](../tabs/design/tabs.md)する : Teams タブを設計する際の推奨ガイドラインを参照してください。
* [モバイル用のタブの作成](../tabs/design/tabs-mobile.md): 携帯電話やタブレットのタブを開発する方法について説明します。
* [Microsoft Graph API を使用して Teams データを利用する](https://docs.microsoft.com/graph/teams-concept-overview)
* [ツールキットを使わずにタブを作成する](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>次のレッスン

コラボレーション用のタブを作成する方法を知っている。 別の種類の Teams アプリを作成する場合

> [!div class="nextstepaction"]
> [Bot を作成する](../build-your-first-app/build-bot.md)
