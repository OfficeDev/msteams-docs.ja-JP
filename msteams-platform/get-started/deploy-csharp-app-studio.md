---
title: App Studio で C# を使用して最初のアプリをデプロイする
description: C# または .NET を使用して Microsoft Teams アプリを展開する方法について説明します。 App Studio で
keywords: .net c# csharp アプリ スタジオの使用を開始する
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.localizationpriority: medium
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 6fa0b290b0d0918c02427959b96eb897931aa4de
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558458"
---
# <a name="update-c-app-package-in-app-studio"></a>App Studio で C# アプリ パッケージを更新する

> [!TIP]
> **開発者ポータルを試す**: App Studio が進化しました。 新しい[開発者ポータル](https://dev.teams.microsoft.com/)を使用して Teams アプリを構成、配布および管理する。

App Studio は、Teams ストアからインストールできる Teams アプリです。 これにより、アプリの作成と登録が簡略化されます。

アプリ パッケージを更新するには、次の手順を実行します。

1. Teams に App Studio をインストールするには、左側のバーの下部にある **[アプリ** ] アイコンを選択し、 **App Studio** を検索します。

    <img  width="450px" alt="Finding App Studio in the Store View" src="~/assets/images/get-started/searchforAppStudio.png"/>

1. **App Studio** タイルを選択し、[**インストール**] を選択します。 App Studio がインストールされます。

    <img  width="450px" alt="Installing App Studio" src="~/assets/images/get-started/InstallingAppStudio.png"/>

1. Teams アプリのアプリ パッケージを作成するには、**App Studio** の **[マニフェスト エディター**] タブを選択します。

    <img  width="450px" alt="App Studio" src="~/assets/images/get-started/AppStudio.png"/>

    このサンプルには独自のマニフェストが付属しており、プロジェクトのビルド時にアプリ パッケージをビルドするように設計されています。 manifest.json ファイルは、マニフェストの Visual Studio の下 ```Microsoft.Teams.Samples.HelloWorld.Web```に配置できます。

     Visual Studio では、manifest.json ファイルは [**マニフェスト**`Microsoft.Teams.Samples.HelloWorld.Web`] の下にあります。 この手順については、次の図を参照してください。  

    <img  width="450px" alt="Build the app package on .NET with Visual Studio" src="~/assets/images/get-started/app-package-on-.NET-with-Visual-Studio.png"/>

1. このアプリ パッケージを変更するには、**マニフェスト エディター** で **[既存のアプリのインポート**] を選択します。

    <img  width="450px" alt="Importing an existing app" src="~/assets/images/get-started/Importinganapp.png"/>

1. 新しくインポートしたアプリの **Hello World** タイルを選択します。

    <img  width="450px" alt="Newly imported app view" src="~/assets/images/get-started/HelloWorldappdetails.png"/>

    次の図は、App Studio でインポートされたアプリ パッケージを示しています。

    <img  width="450px" alt="Importing the app package" src="~/assets/images/get-started/Importinganapp2.png"/>

    マニフェスト エディターの左側には、手順の一覧があります。 右側には、ステップごとに入力する必要があるプロパティの一覧があります。 サンプル アプリを使い始めると、情報の多くが既に完了しています。 次の手順では、Hello World アプリのプロパティを更新できます。

## <a name="app-details"></a>アプリの詳細

[ **詳細] で [アプリの詳細** ] を選択 **します**。 [ **生成** ] ボタンを選択して、新しいアプリ ID を作成します。

新しいアプリ ID は次のようになります `2322041b-72bf-459d-b107-f4f335bc35bd`。

**開発者情報** やブランドの詳細など、右側のウィンドウでアプリの詳細 **を** 確認します。 これらの詳細は、配布用の新しいアプリを作成する場合に重要です。

## <a name="tabs"></a>タブ

Teams アプリにタブを追加するのは簡単です。 サンプル アプリでは既に複数のタブがサポートされており、それらを有効にできます。

### <a name="team-tab"></a>[チーム] タブ

アプリに使用できるチーム タブは 1 つだけです。

<img  width="450px" alt="Adding a Teams tab" src="~/assets/images/get-started/TeamTab.png"/>

このサンプルでは、[チーム] タブに構成ページが表示されます。 **Tab 構成 URL** **の ...** 記号を選択し、ドロップダウン メニューから **[編集]** を選択します。 URL を、アプリを `https://yourteamsapp.ngrok.io/configure` ホストするときに使用した URL に置き換える必要がある場所 `yourteamsapp.ngrok.io` に変更します。

### <a name="personal-tabs"></a>[個人] タブ

アプリには、[チーム] タブを含め、最大 16 個のタブを含めることができます。

個人用タブは、[チーム] タブとは異なります。 **Hello Tab** は、プレースホルダー値 `com.contoso.helloworld.hellotab`を持つ個人用タブの一覧に既に一覧表示されています。 **Tab 構成 URL** **の ...** 記号を選択し、ドロップダウン メニューから **[編集]** を選択します。 次のダイアログ ボックスが表示されます。

<img  width="450px" alt="Adding a personal tab dialog" src="~/assets/images/get-started/PersonalTab.png"/>

アプリの URL で次のボックスを更新します。

- **[コンテンツ URL**] ボックスを [次へ] に変更します。`https://yourteamsapp.ngrok.io/hello`
- [Web サイト URL] ボックスを [ **Web サイトの URL** ] ボックスに変更する `https://yourteamsapp.ngrok.io/hello`

アプリをホストするときに使用した URL で置き換えます `yourteamsapp.ngrok.io` 。

#### <a name="bots"></a>ボット

ボット機能をアプリに簡単に追加できます。 **Hello World** サンプル アプリには、サンプルの一部としてボットが既にありますが、Microsoft に登録する必要があります。

<img  width="450px" alt="Adding a bot" src="~/assets/images/get-started/Bots.png"/>

サンプルからインポートされたボットに、関連付けられているアプリ ID がありません。 App Studio が新しいアプリ ID を作成して Microsoft に登録できるように、新しいボットを作成する必要があります。

> [!NOTE]
> ボット用に App Studio によって作成されたアプリ ID は、アプリ用に作成されたアプリ ID とは異なります。 アプリ内の各ボットには、独自のアプリ ID が必要です。

ボットをセットアップするには、次の手順を実行します。

1. ボットの一覧で、インポートしたボットの横にある **[削除** ] を選択します。 これで、表示するボットは残されていません。
1. [ **セットアップ] を** 選択して、[ **ボットのセットアップ** ] ダイアログ ボックスを表示します。

    <img  width="450px" alt="Adding a bot dialog" src="~/assets/images/get-started/Setupbot.png"/>

1. **ボット名 Contoso ボット** を追加し、[**スコープ**] で 3 つのチェック ボックスをすべてオンにします。
1. **[保存] を** 選択してダイアログ ボックスを終了します。 App Studio は、ボットを Microsoft に登録し、ボットの一覧に新しいボットを表示します。
1. 次に、メモ帳でテキスト ファイルを開き、新しいボット ID をコピーして貼り付けます。
1. [ **新しいパスワードの生成**] をクリックし、ボットアプリ ID をメモしたのと同じテキスト ファイルにパスワードを書き留めます。
1. **ボット エンドポイント アドレス** を`https://yourteamsapp.ngrok.io/api/messages`更新し、アプリをホストするときに使用した URL に置き換えます`yourteamsapp.ngrok.io`。
1. 次に、ボットとの安全な通信を可能にするために、ファイルの情報をホストされたアプリに追加する必要があるため、テキスト ファイルを保存します。

#### <a name="messaging-extensions"></a>メッセージング拡張機能

メッセージ拡張機能を使用すると、ユーザーはサービスから情報を要求し、その情報を投稿できます。 情報は、カードの形式でチャネルの会話に投稿されます。 メッセージ拡張機能は、作成ボックスの下部に表示されます。

メッセージング拡張機能をセットアップするには、次の手順を実行します。

1. App Studio の左側のウィンドウにある **[機能**] で [**メッセージング拡張機能**] を選択して、メッセージング拡張機能を構成します。

    <img  width="450px" alt="Adding a messaging extension" src="~/assets/images/get-started/Messagingextensions.png"/>

    メッセージング拡張機能のサンプルは、[ **メッセージング拡張機能** ] ウィンドウに一覧表示されます。

1. **[削除] を** 選択してメッセージング拡張機能を削除し、[**セットアップ**] を選択し、[ボット](#bots)に使用するのと同じ手順に従います。 [ **メッセージング拡張機能** ] ダイアログ ボックスが表示されます。
1. [ **既存のボットを使用** ] タブを選択し、 **既存のボットの 1 つから選択します**。
1. ドロップダウン メニューから作成したボットを選択します。 **ボット名** を追加し、[**保存]** を選択してダイアログ ボックスを閉じます。
1. **[コマンド**] セクションで、[**追加**] を選択します。 検索ベースのコマンドを追加するには、[ユーザーに **情報の照会とメッセージへの挿入を許可** する] オプションを選択します。
1. [ **新しいコマンド** ] ダイアログ ボックスで、次の値を入力します。

    [ **新しいコマンド] で次のコマンドを実行します**。

    - **コマンド ID**: ランダム テキストを入力する
    - **タイトル**: ランダムなタイトルを入力する
    - **説明**: ランダムな説明を入力します

    [ **パラメーター**] の下:

    - **名前**: パラメーター名を入力します
    - **タイトル**: カードのタイトルを入力します
    - **説明**: カードの説明を入力する

1. 情報を入力したら、[ **保存]** を選択してダイアログ ボックスを閉じます。

#### <a name="register-your-app-in-teams"></a>Teams にアプリを登録する

アプリの詳細を入力したら、次の手順に従って Teams にアプリを登録します。

1. App Studio の **テストと配布** を使用して、Teams にアプリをインストールします。
1. ボットのアプリ ID とパスワードを使用して、ホストされているアプリケーションを更新します。 サンプル アプリの場合は、ボット拡張機能とメッセージング拡張機能の両方に同じアプリ ID とパスワードを使用します。
1. App Studio の左側のウィンドウで、[**完了]** で [**テストと配布**] を選択します。

    <img  width="450px" alt="Testing your app" src="~/assets/images/get-started/Testanddistribute.png"/>

1. アプリを Teams にアップロードするには、**テストと配布** の下にある **[インストール**] ボタンを選択します。

    <img  width="450px" alt="Adding a messaging extension dialog" src="~/assets/images/get-started/InstallingHelloWorld.png"/>

    > [!NOTE]
    > アプリをサイドロードできない場合は、 [カスタム アプリのアップロードを有効に](../get-started/get-started-dotnet-app-studio.md#enable-sideloading-option)しているかどうかを確認します。

1. [**チームに追加**] セクションで **[検索**] ボックスを選択し、サンプル アプリを追加するチームを選択します。 テスト用に特別なチームを設定できます。
1. ダイアログ ボックスの下部にある [ **インストール** ] ボタンを選択します。

    アプリが Teams で利用できるようになりました。 ただし、ホストされているアプリケーション環境をアプリ ID とパスワードで更新するまで、ボットとメッセージング拡張機能は機能しません。

    <img  width="450px" alt="The finished app" src="~/assets/images/get-started/Finishedhelloworld.png"/>

## <a name="register-your-app-in-teams"></a>Teams にアプリを登録する

アプリの詳細を入力したら、次の手順に従って Teams にアプリを登録します。

1. 開発者ポータルの **プレビュー** を使用して、Teams にアプリをインストールします。

    :::image type="content" source="../assets/images/teams-toolkit-v2/preview-in-teams.png" alt-text="[プレビュー] ボタンを示す画像":::

1. ボットのアプリ ID とパスワードを使用して、ホストされているアプリケーションを更新します。 サンプル アプリの場合は、ボット拡張機能とメッセージング拡張機能の両方に同じアプリ ID とパスワードを使用します。

1. [ **発行] を選択して、**  開発者ポータルの左側のウィンドウの [ **発行** ] の下に保存します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/devp-publish-left-pane.png" alt-text="左側のウィンドウの [発行] オプションを示す画像":::

    > [!NOTE]
    > アプリをサイドロードできない場合は、 [カスタム アプリのアップロードを有効に](../get-started/get-started-dotnet-app-studio.md#enable-sideloading-option)しているかどうかを確認します。

1. [ **追加]** を選択して、Teams にアプリをインストールします。

    アプリが Teams で利用できるようになりました。 ただし、ホストされているアプリケーション環境をアプリ ID とパスワードで更新するまで、ボットとメッセージング拡張機能は機能しません。

## <a name="update-the-credentials-for-your-hosted-app"></a>ホストされているアプリの資格情報を更新する

サンプル アプリでは、環境変数をテキスト ファイルに保存した値に設定する必要があります。

1. ソリューション エクスプローラーを開きます。

    :::image type="content" source="../assets/images/get-started/csharp-repo-cloned.png" alt-text="c# Teams アプリのサンプル リポジトリ":::

1. `appsettings.json` ファイルを開きます。

    :::image type="content" source="../assets/images/teams-toolkit-v2/csharp-appsetting-json.png" alt-text="appsettings.json ファイルを示す画像":::

1. テキスト ファイルに保存したボット ID で **MicrosoftAppId** 値を更新します。
1. 保存したボット パスワードで **MicrosoftAppPassword** を更新します。

    :::image type="content" source="../assets/images/get-started/get-started-net-azure-add-keys.png" alt-text="Azure キーの追加を示す画像":::

    これらの変更を行った後、アプリをリビルドします。 ngrok を使用している場合は、アプリをローカルで実行し、Azure でホストしている場合はアプリを再デプロイします。

## <a name="test-the-app-capabilities-in-teams"></a>Teams でアプリの機能をテストする

### <a name="test-your-tab"></a>タブをテストする

Teams にアプリをインストールしたら、アプリを読み込むタブを表示するように構成します。

[アプリ] タブを構成するには:

1. サンプル アプリをインストールしたチームのチャネルに移動し、[ **+]** ボタンを選択して新しいタブを追加します。
1. タブ **の** 追加リストからHello World **を** 選択します。 このチャネルに表示するタブを選択できる構成ダイアログ ボックスが表示されます。
1. **[保存]** を選択します。 タブには `Hello World` タブが読み込まれます。

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>Teams でボットをテストする

これで、Teams でボットをテストできるようになりました。

ボットをテストするには:

- アプリを登録したチームでチャネルを選択し、入力します `@your-bot-name`。 この種類のメッセージは **メンションと呼ばれます\@**。 ボットは、送信したメッセージに返信します。

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>メッセージング拡張機能をテストする

メッセージング拡張機能をテストするには:

1. 会話ビューの入力ボックスの下にある **[..** . ] を選択します。 **'Hello World'** アプリのメニューが表示されます。
1. メニューを選択すると、ランダムなテキストのセットが表示されます。 ランダムなテキストの 1 つを選択し、会話に挿入することができます。

    <img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. ランダム テキストのいずれかを選択します。 フォーマットされ、独自のメッセージで送信する準備が整ったカードが表示されます。

    <img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

| &nbsp; | &nbsp; |
|:--- | ---:|
|[Back](get-started-overview.md) | &nbsp; |
|
