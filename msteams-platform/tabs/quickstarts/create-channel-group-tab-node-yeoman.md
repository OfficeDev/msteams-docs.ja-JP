---
title: Node.js と Microsoft Teams 用のごみ箱のジェネレーターを使用して、カスタムのチャネルとグループタブを作成する
author: laujan
description: Microsoft Teams 用のごみ箱のジェネレーターを使用して、チャネルおよびグループタブを作成するためのクイックスタートガイド。
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 77081f83c753f812032ccfebe2accd3cb8859f99
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818935"
---
# <a name="create-a-custom-channel-and-group-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Node.js と Microsoft Teams 用のごみ箱のジェネレーターを使用して、カスタムのチャネルとグループタブを作成する

>[!NOTE]
>このクイックスタートは、「Microsoft OfficeDev GitHub リポジトリにある [最初の Microsoft Teams アプリ](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki を構築する」に記載されている手順に従います。

このクイックスタートでは、Teams の [ [オマーン] ジェネレーター](https://github.com/OfficeDev/generator-teams/)を使用して、カスタムのチャネルとグループタブを作成する手順を順を追って説明します。

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**構成可能なタブまたは静的タブを作成しますか?**

方向キーを使用して、[構成可能なタブ] を選択します。

**タブに使用するスコープを決定します。**

チームまたはグループチャット (あるいはその両方) を選択できます。

**このタブを SharePoint Online で使用できるようにしますか。(Y/n)** 

[ **N**] を選択します。

>[!IMPORTANT]
>このクイックスタートで参照される path コンポーネントの **Defaulttabnametab**は、[ **既定のタブ名** ] と [word **] タブ**に入力した値です。
>
>例: defaulttabname: **MyTab**/  =>  **mytabtab/**

プロジェクトディレクトリで、次の場所に移動します。

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

ここでは、タブロジックについて説明します。 メソッドを検索 `render()` し、次の `<div>` タグとコンテンツをコンテナーコードの先頭に追加し `<PanelBody>` ます。

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

更新したファイルを保存してください。

## <a name="build-and-run-your-application"></a>アプリケーションをビルドして実行する

プロジェクトディレクトリでコマンドプロンプトを開いて、次のタスクを完了します。

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

[タブの構成] ページを表示するには、に移動 `https://localhost:3007/<yourDefaultAppNameTab>/config.html` します。 以下のように表示されます。

![構成ページのスクリーンショット](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルの確立

Microsoft Teams は完全なクラウドベースの製品であり、HTTPS エンドポイントを使用してクラウドからタブのコンテンツを利用できるようにする必要があります。 Teams ではローカルホスティングが許可されていません。そのため、タブをパブリック URL に公開するか、またはプロキシを使用して、ローカルポートをインターネットに接続する URL に公開する必要があります。

タブ拡張機能をテストするには、このアプリケーションに組み込まれている [ngrok](https://ngrok.com/docs)を使用します。 Ngrok はリバースプロキシソフトウェアツールであり、ローカルで実行されている web サーバーの公開された HTTPS エンドポイントへのトンネルを作成します。 サーバーの web エンドポイントは、ローカルコンピューターの現在のセッション中に使用できるようになります。 コンピューターがシャットダウンされるかスリープ状態になると、サービスは使用できなくなります。

コマンドプロンプトで、localhost を終了し、次のように入力します。

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> タブが Microsoft teams にアップロードされて正常に保存されると、タブギャラリーで表示し、[タブ] バーに追加して、ngrok トンネルセッションが終了するまでそれを操作することができます。 Ngrok セッションを再起動する場合は、新しい URL を使用してアプリを更新する必要があります。

## <a name="upload-your-application-to-teams"></a>アプリケーションを Teams にアップロードする

- Microsoft Teams クライアントを開きます。 [Web ベースのバージョン](https://teams.microsoft.com)を使用する場合は、ブラウザーの[開発者ツール](~/tabs/how-to/developer-tools.md)を使用してフロントエンドコードを調べることができます。
- 左側の [ *チーム* ] パネルで、 `...` 使用しているチームの横のメニューを選択して、タブのテストを行い、[ **チームの管理**] を選択します。
- メインパネルで、タブバーから [ **アプリ** ] を選択し、ページの右下隅にある [ **カスタムアプリのアップロード** ] を選択します。
- プロジェクトディレクトリを開き、 **./パッケージ** フォルダーを参照して、アプリパッケージの zip フォルダーを選択し、[ **開く**] を選択します。 タブが Teams にアップロードされます。
- チームに戻り、タブを表示するチャネルを選択し、タブバーから [➕] を選択して、ギャラリーからタブを選択します。
- タブを追加する手順に従います。[チャネル/グループ] タブには、カスタム構成ダイアログがあることに注意してください。
- [ **保存** ] を選択すると、タブがチャネルのタブバーに追加されます。
