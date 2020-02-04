---
title: 'クイックスタート: node.js を使用してカスタムの個人用タブを作成し、Microsoft Teams 用の Outlook を使用します。'
author: laujan
description: Microsoft Teams 用のごみ箱のジェネレーターを使用して、個人用タブを作成するためのクイックスタートガイド。
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 2d1b17360b92a161179091c1f6ba06ffa194e958
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674618"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>クイックスタート: node.js を使用してカスタムの個人用タブを作成し、Microsoft Teams 用の Outlook を使用します。

>[!NOTE]
>このクイックスタートは、「Microsoft OfficeDev GitHub リポジトリにある[最初の Microsoft Teams アプリ](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)Wiki を構築する」に記載されている手順に従います。

このクイックスタートでは、Teams の [[オマーン] ジェネレーター](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)を使用して、カスタムの個人用タブを作成する手順を順を追って説明します。 また、アプリケーションをチームにアップロードします。

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**構成可能なタブまたは静的タブを作成しますか?**

方向キーを使用して、[静的] タブを選択します。

>[!IMPORTANT]
>このクイックスタートで参照される path コンポーネントの*Defaulttabnametab*は、[*既定のタブ名*] と [word *] タブ*に入力した値です。
>
>例: defaulttabname: *MyTab* => /*mytabtab/*

## <a name="create-your-personal-tab"></a>[個人用] タブを作成する

このアプリケーションに個人用タブを追加するには、コンテンツページを作成し、既存のファイルを更新します。

- コードエディター**で、新しい html ファイル (.html** ) を作成し、次のマークアップを追加します。

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>
            <!-- Todo: add your a title here -->
        </title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <!-- inject:css -->
        <!-- endinject -->
    </head>
        <body>
            <h1>Personal Tab</h1>
            <p><img src="/assets/icon.png"></p>
            <p>This is your personal tab!</p>
        </body>
</html>
```

- アプリケーションの**web**フォルダーに**personal .html**を保存します。

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- コードエディターで**マニフェスト**を開きます。

```bash
./src/manifest/manifest.json/
```

次のものを空`staticTabs`の配列 (`staticTabs":[]`) に追加し、次の JSON オブジェクトを追加します。

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

「 **Defaulttabnametab** 」という実際のタブ名を使用して、 **「contenturl」** パスコンポーネントを必ず更新してください。

- 更新された**manifest**を保存します。

- コンテンツページは IFrame で提供される必要があります。 コードエディターで、次のように Tab を開きます **。**

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- 次のものを IFrame decorators のリストに追加します。

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- 更新した**タブの ts**ファイルを保存してください。 タブコードが完成しました。

## <a name="build-and-run-your-application"></a>アプリケーションをビルドして実行する

プロジェクトディレクトリでコマンドプロンプトを開いて、次のタスクを完了します。

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

[個人用] タブを表示するには、`http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![[個人用] タブのスクリーンショット](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルの確立

Microsoft Teams は完全なクラウドベースの製品であり、HTTPS エンドポイントを使用してクラウドからタブのコンテンツを利用できるようにする必要があります。 Teams ではローカルホスティングが許可されていません。そのため、タブをパブリック URL に公開するか、またはプロキシを使用して、ローカルポートをインターネットに接続する URL に公開する必要があります。

タブ拡張機能をテストするには、このアプリケーションに組み込まれている[ngrok](https://ngrok.com/docs)を使用します。 Ngrok はリバースプロキシソフトウェアツールであり、ローカルで実行されている web サーバーの公開された HTTPS エンドポイントへのトンネルを作成します。 サーバーの web エンドポイントは、ローカルコンピューターの現在のセッション中に使用できるようになります。 コンピューターがシャットダウンされるかスリープ状態になると、サービスは使用できなくなります。

コマンドプロンプトで、localhost を終了し、次のように入力します。

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> タブが Microsoft teams にアップロードされ、 *ngrok*を介して正常に保存されると、トンネルセッションが終了するまで、teams でそのタブを表示することができます。

## <a name="upload-your-application-to-teams"></a>アプリケーションを Teams にアップロードする

- Microsoft Teams クライアントを開きます。 [Web ベースのバージョン](https://teams.microsoft.com)を使用する場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンドコードを調べることができます。
- 左側の [*チーム*] パネルで、使用して`...`いるチームの横のメニューを選択して、タブのテストを行い、[**チームの管理**] を選択します。
- メインパネルで、タブバーから [**アプリ**] を選択し、ページの右下隅にある [**カスタムアプリのアップロード**] を選択します。
- プロジェクトディレクトリを開き、 **./パッケージ**フォルダーを参照し、zip フォルダーを選択して右クリックし、[**開く**] を選択します。 タブが Teams にアップロードされます。

## <a name="view-your-personal-tabs"></a>個人用タブの表示

Teams クライアントの左端にあるナビゲーションバーで、 `...`メニューを選択し、リストからアプリを選択します。
