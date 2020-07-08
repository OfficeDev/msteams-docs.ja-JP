---
title: Microsoft Teams Toolkit と Visual Studio コードを使用してアプリをビルドする
description: Microsoft Teams ツールキットを使用して、Visual Studio Code 内で魅力的なカスタムアプリを直接作成する
keywords: teams visual studio code toolkit
ms.date: 06/30/2020
ms.openlocfilehash: 17f21d1656b32074318030b9df9e643200f58f80
ms.sourcegitcommit: ecf7ca8e77e77fe3f4cad1b13e3d31a825155555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "45054253"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio-code"></a>Microsoft Teams Toolkit と Visual Studio コードを使用してアプリをビルドする

Microsoft Teams Toolkit を使用すると、カスタム Teams アプリを Visual Studio Code 環境内で直接作成することができます。 このツールキットは、このプロセスを順を追って説明しており、Teams アプリを構築、デバッグ、および起動するために必要なすべての情報を提供します。

## <a name="installing-the-teams-toolkit"></a>Teams ツールキットをインストールする

Microsoft Teams Toolkit for Visual studio code は、visual [Studio Marketplace](https://aka.ms/teams-toolkit)からダウンロードするか、Visual studio code 内の拡張機能として直接ダウンロードできます。

> [!TIP]
> インストール後に、Visual Studio Code アクティビティバーに Teams ツールキットが表示されます。 表示されていない場合は、アクティビティバー内を右クリックし、[ **Microsoft Teams** ] を選択して、簡単にアクセスできるようにツールキットを固定します。

## <a name="using-the-toolkit"></a>ツールキットの使用

- [新しいプロジェクトをセットアップする](#set-up-a-new-teams-project)
- [既存のプロジェクトをインポートする](#import-an-existing-teams-app-project)
- [アプリを構成する](#configure-your-app)
- [アプリをパッケージ化する](#package-your-app)
- [Teams でアプリを実行する](#run-your-app-in-teams)
- [アプリを検証する](#validate-your-app)
- [アプリを発行する](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>新しい Teams プロジェクトをセットアップする

1. ローカル環境でプロジェクトのワークスペース/フォルダーを作成します。
1. Visual Studio Code で、Teams アイコンを選択します。 ![Teams アイコン](../assets/icons/favicon-16x16.png) ウィンドウの左側にあるアクティビティバーから。
1. [コマンド] メニューから [ **Microsoft Teams Toolkit** ] を選択します。
1. [コマンド] メニューから [**新しい Teams アプリの作成**] を選択します。
1. メッセージが表示されたら、ワークスペースの名前を入力します。 これは、プロジェクトが存在するフォルダーの名前と、アプリの既定の名前の両方として使用されます。
1. **Enter**キーを押すと、[**機能の追加**] 画面が表示され、新しいアプリのプロパティを構成します。
1. [**完了**] ボタンを選択して、構成プロセスを完了します。

## <a name="import-an-existing-teams-app-project"></a>既存の Teams アプリプロジェクトをインポートする

1. Visual Studio Code で、Teams アイコンを選択します。 ![Teams アイコン](../assets/icons/favicon-16x16.png) ウィンドウの左側にあるアクティビティバーから。
1. [コマンド] メニューから [**アプリパッケージのインポート**] を選択します。
1. 既存の[Teams アプリパッケージ](../concepts/build-and-test/apps-package.md)の zip ファイルを選択します。
1. **[発行パッケージの選択**] ボタンを選択します。 これで、ツールキットの [構成] タブにアプリの詳細が設定されます。
1. Visual studio code で、[**ファイル**] [  ->  **ワークスペースへのフォルダーの追加**] を選択して、ソースコードディレクトリを visual studio code Workspace に追加します。

## <a name="configure-your-app"></a>アプリを構成する

主に、Teams アプリは3つのコンポーネントをサポートしています。

  1. ユーザーがアプリを操作する Microsoft Teams クライアント (web、デスクトップ、またはモバイル)。
  1. Teams に表示されるコンテンツの要求に応答するサーバー。たとえば、HTML タブのコンテンツや bot のアダプティブカード。
  1. 3つのファイルで構成される Teams[アプリパッケージ](/concepts/build-and-test/apps-package.md):

  > [!div class="checklist"]
  >
  > - manifest.js 
  > - パブリックまたは組織のアプリカタログに表示するための、アプリの[カラーアイコン](../resources/schema/manifest-schema.md#icons)
 > - Teams アクティビティバーに表示するための[アウトラインアイコン](../resources/schema/manifest-schema.md#icons)。

アプリがインストールされると、Teams クライアントはマニフェストファイルを解析して、アプリの名前やサービスが配置されている URL などの必要な情報を特定します。

1. アプリを構成するには、Visual Studio Code の [ **Microsoft Teams Toolkit** ] タブに移動します。
1. [**アプリパッケージの編集**] を選択して、[**アプリの詳細**] ページを表示します。
1. [アプリの詳細] ページのフィールドを編集すると、最終的にアプリパッケージの一部として配布されるファイルの manifest.jsの内容が更新されます。 [詳細情報](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>アプリをパッケージ化する

**アプリの詳細**ページを変更するか、**マニフェスト**を更新するか、またはアプリの**publish**フォルダー内の**env**ファイルを変更すると、 **Development.zip**ファイルが自動的に生成されます。 同じフォルダーに[2 つのアイコン](../concepts/build-and-test/apps-package.md#icons)を含める必要があります。

## <a name="install-and-run-your-app-locally"></a>アプリをローカルにインストールして実行する

アプリのパッケージ化とテストの詳細な手順については、「プロジェクトホームページのコンテンツを*ビルドして実行*する」を参照してください。 一般に、アプリのサーバーをインストールし、実行して、トンネリングソリューションをセットアップして、Teams が localhost から実行されているコンテンツにアクセスできるようにする必要があります。

## <a name="add-a-trusted-certificate-for-localhost"></a>Localhost の信頼できる証明書を追加する

Https を使用して localhost でタブベースのアプリをデバッグする場合は、localhost の証明書を catalog に追加する必要があり `Trusted Root Certification Authorities` ます。 この手順は、コンピューターごとに1回だけ実行する必要があります。</br></br>

**信頼できる証明書を作成してインストールします。**
<details>
  <summary>展開する場所</summary>

* アプリの作成と実行
  * プロジェクト Readme の「**ビルドと実行**」セクションの instuctions に従って、そのサービスが提供されるように https://localhost:3000/tab します。一般的には、次のようにして実行します。 `npm install``npm start`
  * https://localhost:3000/tabGoogle Chrome から移動します

* SSL 証明書を取得します。
  * [Chrome 開発者ツール] ウィンドウ () を開き `ctrl + shift + i`  /  `cmd + option + i` ます。
  * タブをクリックします。 `Security`
  * [] `View certificate` をクリックすると、OS X でデスクトップに証明書をドラッグするか、または Windows のタブをクリックして、次のボタンをクリックすることによって、証明書をダウンロードすることができます。 `Details``Copy to File…`
  * ファイルに*任意*の> <名前を付け、書き込み操作を実行するために管理者の同意を必要としないフォルダーに保存します。
  
* **Windows**に証明書をインストールする
  * `DER encoded binary X.509 (.CER)`オプション (最初の1つ) を選択し、保存します。
  * 証明書をダブルクリックしてインストールします。
  * [`Local Machine`
  * 選択`Place all certificates in the following store`
  * [`Trusted Root Certification Authorities`
  * インストールを確認する
  
* **MAC OS X**の証明書をインストールする
  * OS X で、キーチェーンアクセスユーティリティを開き、 `System` 左側のメニューから選択します。 ロックアイコンをクリックして、変更を有効にします。
  * 下部にあるプラスボタンをクリックして新しい証明書を追加し、 `localhost.cer` デスクトップにドラッグしたファイルを選択します。 `Always Trust`表示されるダイアログボックスをクリックします。
  * システムキーチェーンに証明書を追加した後、証明書をダブルクリックして、[ `Trust` 証明書の詳細] セクションを展開します。 [ `Always Trust` すべて] オプションを選択します。

> [!IMPORTANT]
> セキュリティ証明書の警告が表示された場合は、に移動 https://localhost:3000/tab します。サイトが依然として信頼されていない場合は、コンピューターを再起動し、localhost を信頼できるユーザーとして承認する必要があります。
</details>

## <a name="run-your-app-in-teams"></a>Teams でアプリを実行する
- 前提条件:
  - [Teams 開発者プレビューモードを有効にする](https://aka.ms/teams-toolkit-enable-devpreview)

1. Visual Studio の [コード] ウィンドウの左側にあるアクティビティバーに移動します。
1. [実行 **] アイコンを**選択して、[**実行] および [デバッグ**] ビューを表示します。
1. キーボードショートカットを使用することもでき `Ctrl+Shift+D` ます。

## <a name="validate-your-app"></a>アプリを検証する

[**検証**] ページでは、アプリを appsource に提出する前にアプリパッケージを確認できます。 マニフェストパッケージをアップロードすると、検証ツールによって、マニフェスト関連のすべてのテストケースに対してアプリがチェックされます。 失敗した各テストの説明には、エラーを解決するためのドキュメントリンクが記載されています。 自動化が困難なテストの場合、最も一般的な失敗したテストケースの7つの**事前チェックリスト**と、完全な提出チェックリストへのリンクがあります。

## <a name="publish-your-app-to-teams"></a>アプリを Teams に公開する

プロジェクトのホームページでは、アプリをチームにアップロードしたり、アプリを組織内のユーザーに対して会社のカスタムアプリストアに提出したり、アプリをアプリソースに提出してすべての Teams ユーザーに提供したりすることができます。 IT 管理者は、これらの送信を確認します。 [*発行*] ページに戻り、送信の状態を確認し、アプリが IT 管理者によって承認または拒否されたかどうかを確認することができます。これは、アプリに更新を送信するか、現在アクティブな提出を取り消すこともできます。

> [!div class="nextstepaction"]
> [次のステップ: 公開アプリの管理とサポート](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
