---
title: Node.jsとヨーマンジェネレータを使用したカスタムチャンネルとグループタブを作成Microsoft Teams
author: laujan
description: Microsoft Teams用の Yeoman ジェネレータを使用してチャネルとグループ タブを作成するクイック スタート ガイドです。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 559393884e3b8a4aad1787ea4ca8f9f4de54d151
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566647"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Node.jsとYeoman ジェネレータを使用して、カスタムチャネルとグループタブを作成Microsoft Teams

>[!NOTE]
>このクイック スタートは、Microsoft OfficeDev GitHub リポジトリにある[最初のMicrosoft Teams アプリ](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)Wiki で説明されている手順に従います。

このクイック スタートでは、 [Yeoman ジェネレーター を](https://github.com/OfficeDev/generator-teams/)使用してカスタム チャネルとグループ タブを作成する方法Teamsします。

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**構成可能なタブまたは静的タブを作成しますか?**

矢印キーを使用して、構成可能なタブを選択します。

**Tab に使用するスコープを指定してください。**

チームチャットやグループチャットを選択できます。

**このタブをオンラインで使用できるようにしますSharePoint?(Y/n)** 

n を選択します。

>[!IMPORTANT]
>このクイック スタートで参照されているパス コンポーネント **の DefaultTabNameTab** は、ジェネレータで **[既定のタブ名]** に入力した値 **と、Tab** という語を使用して入力した値です。
>
>たとえば、デフォルトタブ名:**マイタブ**  =>  **/マイタブタブ/**

プロジェクト ディレクトリで、次のディレクトリに移動します。

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

そこでタブロジックを見つけることができます。 メソッドを探 `render()` し、次の `<div>` タグとコンテンツをコンテナー コードの先頭に追加 `<PanelBody>` します。

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

更新されたファイルを保存してください。

## <a name="build-and-run-your-application"></a>アプリケーションのビルドと実行

プロジェクト ディレクトリでコマンド プロンプトを開き、次のタスクを完了します。

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

タブの構成ページを表示するには、 に移動 `https://localhost:3007/<yourDefaultAppNameTab>/config.html` します。 以下のように表示されます。

![構成ページのスクリーンショット](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへの安全なトンネルを確立する

Microsoft Teamsは完全にクラウドベースの製品であり、HTTPS エンドポイントを使用してクラウドからタブ コンテンツを利用できるようにする必要があります。 Teamsローカル ホスティングを許可しないため、タブをパブリック URL に公開するか、インターネットに接続する URL にローカル ポートを公開するプロキシを使用する必要があります。

タブ拡張をテストするには、このアプリケーションに組み込まれている [ngrok](https://ngrok.com/docs)を使用します。 Ngrok はリバース プロキシ ソフトウェア ツールで、ローカルで実行されている Web サーバーの一般に公開されている HTTPS エンドポイントへのトンネルを作成します。 サーバーの Web エンドポイントは、ローカル コンピューター上の現在のセッション中に使用できます。 マシンがシャットダウンまたはスリープ状態になると、サービスは利用できなくなります。

コマンド プロンプトで localhost を終了し、次のように入力します。

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> タブが Microsoft チームにアップロードされ、正常に保存された後、タブ ギャラリーで表示し、タブ バーに追加して、ngrok トンネル セッションが終了するまで操作できます。 ngrok セッションを再開する場合は、新しい URL でアプリを更新する必要があります。

## <a name="upload-your-application-to-teams"></a>アプリケーションをTeamsにアップロードする

- Microsoft Teams クライアントを開きます。 Web ベースの [バージョン](https://teams.microsoft.com) を使用する場合は、ブラウザーの [開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンド コードを検査できます。
- 左側の *[YourTeams]* パネルで、 `...` タブのテストに使用しているチームの横にあるメニューを選択し、[ **チームの管理**]を選択します。
- メインパネルでタブバーから **「アプリ**」を選択し、ページの右下隅にある **カスタムアプリアップロード** 選択します。
- プロジェクト ディレクトリを開き **、./package** フォルダを参照し、アプリ パッケージの zip フォルダーを選択して 、[ **開く**] を選択します。 タブがTeamsにアップロードされます。
- チームに戻り、タブを表示するチャンネルを選択し、タブバーから➕選択して、ギャラリーからタブを選択します。
- タブを追加する手順に従います。チャンネル/グループタブにはカスタム設定ダイアログがあります。
- [ **保存]** を選択すると、チャンネルのタブバーにタブが追加されます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ASP.NETCore を使用してカスタム チャネルとグループ タブを作成する](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)