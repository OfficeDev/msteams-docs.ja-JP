---
title: チュートリアル - Yeoman ジェネレーターを使用して最初のアプリを作成する
description: Yeoman ジェネレーターを使用して Microsoft Teams アプリの構築を開始する方法について説明します。
keywords: nodejs yeoman node.jsの開始
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: f7f0fb3ba1be28dfa7d343be3af9d122b4ad090d
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037005"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>Yeoman ジェネレーターを使用して最初の Microsoft Teams アプリを作成する

>[!Note]
>このチュートリアルは [、Teams Wiki 用の Yeoman ジェネレーターから提供されます](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。

このチュートリアルでは、Microsoft Teams Yeoman ジェネレーターを使用して最初の Microsoft Teams アプリを作成する方法について説明します。 アプリのサイドローディングを許可する Teams アカウント [を持っている必要があります](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

![yeoman ジェネレーター git](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>コンピューターのセットアップと準備

Yeoman ジェネレーターの使用を開始する前に、コンピューターに以下をインストールする必要があります。

### <a name="install-nodejs"></a>Node.js. のインストール

コンピューターにインストールNode.js必要があります。 最新の [LTS バージョンを使用する必要があります](https://nodejs.org)。

### <a name="install-a-code-editor"></a>コード エディターのインストール

コード エディターも必要です。好きなテキスト エディターを自由に使用できます。 ただし、このドキュメントとスクリーンショットの大部分は、コードのVisual Studio [しています](https://code.visualstudio.com)。

### <a name="install-yeoman-and-gulp-cli"></a>Yeoman と Gulp CLI をインストールする

Teams ジェネレーターを使用してプロジェクトをスキャフォールディングするには、Yeoman ツールと Gulp CLI タスク マネージャーをインストールする必要があります。

コマンド プロンプトを開き、次のコマンドを入力します。

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a>ジェネレーターをインストールする

次のコマンドを使用して、Teams Yeoman ジェネレーターをインストールします。

```bash
npm install generator-teams --global
```

ジェネレーターのプレビュー バージョンをインストールするには、次のコマンドを実行します。

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>プロジェクトを生成する

コマンド プロンプトを開き、プロジェクトを作成する新しいディレクトリを作成し、そのディレクトリでコマンドを実行します `yo teams` 。

これによりジェネレーターが起動し、一連の質問を求めるメッセージが表示されます。

![yo teams](~/assets/yeoman-images/teams-first-app-1.png)

最初の質問はプロジェクト名に関する質問です。Enter キーを押すとそのまま残しておきます。 次の質問では、新しいディレクトリを作成するか、現在のディレクトリを使用するかが問い合されます。 必要なディレクトリに既に存在する場合は、Enter キーを押します。

次の手順では、プロジェクトのタイトルを求めるメッセージが表示されます。このタイトルは、アプリのマニフェストと説明で使用されます。 次に、会社名を入力する必要があります。この名前はマニフェストでも使用されます。

5 番目の質問では、使用するマニフェストのバージョンについて確認します。 このチュートリアルでは、現在 `v1.5` 一般に使用可能なスキーマを選択します。

この後、ジェネレーターはプロジェクトに追加するアイテムを求めるダイアログを表示します。 1 つのアイテムまたはアイテムの任意の組み合わせを選択できます。 For now, just select *a Tab*.

![項目の選択](~/assets/yeoman-images/teams-first-app-2.png)

選択した項目に基づいて、一連のフォローアップ質問が表示されます。

次に、ソリューションをホストする場所の URL を入力する必要があります。 任意の URL を使用できますが、既定ではジェネレーターは Azure Web サイトの URL を提案します。

ジェネレーターには、オプトインまたはオプトアウトできる多くの組み込みの高度な機能があります。 ソリューションに単体テストを含める場合は、URL に関する質問に従って、既定値は yes です。 これを選択すると、生成されたプロジェクトには単体テスト フレームワークと、スキャフォールディングされるさまざまなアイテムに対する既定の単体テストが含まれます。 このチュートリアルでは、テスト フレームワークを含めない選択をします。

ログを簡単に作成するために、ログに Azure Application Insights を使用する必要がある場合も尋ねられる必要があります。 [はい] を選択した場合は、Azure Application Insights キーを指定する必要があります。 このチュートリアルでは、Application Insights の使用をオプトアウトします。

次の質問のセットは、以前に選択した項目に基づいて行います。 タブの場合は、名前を指定し、必要に応じて、このアプリを SharePoint Online Web パーツとして使用する場合に選択する必要があります。 この名前を指定すると、ジェネレーターはプロジェクトを生成し、すべての依存関係をインストールします。 これには 1 分から 2 分かかる場合があります。

## <a name="add-some-code-to-your-tab"></a>タブにコードを追加する

ジェネレーターが完了したら、お気に入りのコード エディターでソリューションを開くことができます。 少し時間を取って、コードの編成方法を理解してください。詳細については、「プロジェクト構造」のドキュメントを [参照](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure) してください。

Tab キーはファイルに保存 `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` されます。 これは、Tab の TypeScript React ベースのクラスです。次のように、メソッドを見つけて、コントロール内にコード行 `render()` `<PanelBody>` を追加します。

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

ファイルを保存し、コマンド プロンプトに戻る。

## <a name="build-your-app"></a>アプリを作成する

これで、プロジェクトをビルドできます。 これは、2 つの手順 (または 1 つの手順、以下を参照) で行います。

まず、Microsoft Teams にアップロードまたはサイドロードする Teams アプリ マニフェスト ファイルを作成する必要があります。 これは、Gulp タスクによって行われます `gulp manifest` 。 これにより、マニフェストが検証され、ディレクトリに zip ファイルが作成 `./package` されます。

ソリューションをビルドするには、コマンドを使用 `gulp build` します。 これにより、ソリューションがフォルダーにトランスピタイル `./dist` されます。 

## <a name="run-your-app"></a>アプリを実行する

アプリを実行するには、コマンドを使用 `gulp serve` します。 これにより、アプリをテストするためのローカル Web サーバーが構築され、開始されます。 また、プロジェクトにファイルを保存するたびに、このコマンドによってアプリケーションが再構築されます。 

これで、タブが表示されているの `http://localhost:3007/myFirstAppTab/` を確認するために参照できる必要があります。 ただし、Microsoft Teams にはまだありません。

![ブラウザーでサイトを表示する](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>Microsoft Teams でアプリを実行する

Microsoft Teams では、アプリを localhost でホストすることはできません。そのため、アプリをパブリック URL に公開するか、ngrok などのプロキシを使用する必要があります。

良いニュースは、スキャフォールディングされたプロジェクトにこの組み込みがあります。 ngrok サービスを実行すると、一意のパブリック DNS エントリを使用してバックグラウンドで開始され、その一意の URL でマニフェストがパッケージ化され、同じことを実行 `gulp ngrok-serve` します `gulp serve` 。

After `gulp ngrok-serve` running, create a new Microsoft Teams team and when it is created click on the Team name, to go to the teams settings and then select *Apps*. 右下隅に[カスタム アプリをアップロードする] リンクが表示されます。それを選択して、プロジェクト フォルダーと呼ばれるサブフォルダーを参照します `package` 。 そのフォルダー内の zip ファイルを選択し、[開く] を選択します。 これで、アプリは Microsoft Teams にサイドローディングされます。

![サイドローディングされたアプリ](~/assets/yeoman-images/teams-first-app-4.png)

[全般] チャネル *に戻* り、選択して *+* 新しいタブを追加します。タブの一覧にタブが表示されます。

![タブを構成する](~/assets/yeoman-images/teams-first-app-5.png)

タブを選択し、指示に従って追加します。 ソースを編集できるカスタム構成ダイアログがあります。 [ *保存] を* 選択して、チャネルにタブを追加します。 完了すると、Microsoft Teams 内にタブが読み込まれます。

![チームでのタブの実行](~/assets/yeoman-images/teams-first-app-6.png)

**おめでとうおめでとう!最初の Microsoft Teams アプリを構築して展開した**
