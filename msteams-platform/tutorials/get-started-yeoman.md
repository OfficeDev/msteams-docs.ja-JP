---
title: チュートリアル - Yeomanジェネレータを使用して最初のアプリを作成します
description: Yeoman ジェネレータを使用してMicrosoft Teamsアプリの構築を開始する方法について説明します。
keywords: ノードス・ヨーマンnode.js始める
localization_priority: Normal
ms.topic: tutorial
ms.custom: scenarios:getting-started
ms.openlocfilehash: 96a4f64d487e1d16bf25abd978759fedeac1061c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566825"
---
# <a name="create-your-first-microsoft-teams-app-using-the-yeoman-generator"></a>ヨーマンジェネレータを使用して、あなたの最初のMicrosoft Teamsアプリを作成します

> [!Note]
> このチュートリアルでは、[ウィキのヨーマンジェネレータTeams提供しています](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)。

このチュートリアルでは、Microsoft Teams Yeoman ジェネレータを使用して、非常に最初のMicrosoft Teamsアプリを作成する手順を説明します。 また、Yeoman ジェネレータを使用してTeamsをアップグレードするプロセスについても説明します。 このチュートリアルで開始する前提条件は、[アプリのサイドローディング](~/concepts/build-and-test/prepare-your-o365-tenant.md)を可能にするTeamsアカウントを持っているということです。

![ヨーマンジェネレータギット](~/assets/yeoman-demo.gif)

## <a name="setup-and-prepare-your-machine"></a>マシンのセットアップと準備

Yeoman ジェネレータを使用する前に、次の機器をマシンにインストールする必要があります。

### <a name="install-nodejs"></a>Node.js. のインストール

マシンにNode.jsをインストールする必要があります。 最新の [LTS バージョン](https://nodejs.org)を使用する必要があります。

### <a name="install-a-code-editor"></a>コード エディターのインストール

コード エディターが必要です。 このドキュメントとイメージのほとんどは、 [Visual Studio Code](https://code.visualstudio.com)を使用して参照しています。 ただし、好きなテキスト エディタを自由に使用してください。

### <a name="install-yeoman-and-gulp-cli"></a>ヨーマンとGulp CLIをインストールする

ジェネレータを使用してプロジェクトをスキャフォールディングするには、Yeoman ツールと Gulp CLI タスクマネージャーをインストールする必要があります。

コマンド プロンプトを開き、次のように入力します。

```bash
npm install yo gulp-cli --global
```

## <a name="install-the-generator"></a>ジェネレーターをインストールする

次のコマンドで Teams Yeoman ジェネレーターをインストールします。

```bash
npm install generator-teams --global
```

次のコマンドを使用して、ジェネレータのプレビュー バージョンをインストールします。

```bash
npm install generator-teams@preview --global
```

## <a name="generate-your-project"></a>プロジェクトを生成する

このセクションでは、プロジェクトを生成する手順について説明します。

**プロジェクトを生成するには**

1. コマンド プロンプトを開き、プロジェクトを作成するディレクトリを新しく作成し、そのディレクトリでコマンドを実行 `yo teams` します。 ジェネレータが起動します。
1. ジェネレータによって促される一連の質問に答えます。

   ![ヨーチーム](~/assets/yeoman-images/teams-first-app-1.png)

   1. 最初の質問は、プロジェクト名についてです、あなたはEnterキーを押すことによって、そのままにしておくことができます。
   1. 次の質問では、新しいディレクトリを作成するか、現在のディレクトリを使用するかを尋ねます。 あなたが望むディレクトリにすでにあるので、単にEnterキーを押してください。
   1. 次の質問で、プロジェクトのタイトルを入力します。 このタイトルは、アプリのマニフェストと説明で使用されます。 
   1. 次に、マニフェストでも使用される会社名を尋ねられます。
   1. 5 番目の質問では、使用するマニフェストのバージョンについて尋ねられています。 このチュートリアルでは、 `v1.5` 現在使用可能な一般的なスキーマである を選択します。
   1. 次に、ジェネレータは、プロジェクトに追加する項目を尋ねます。 1 つまたは任意の組み合わせの項目を選択できます。 このチュートリアルでは、 *タブを* 選択するだけです:

    ![品目の選択](~/assets/yeoman-images/teams-first-app-2.png)

1. 手順 2 で選択した項目に基づいて表示される、次のフォローアップの質問に回答します。
1. ソリューションをホストする URL を入力します。 

   > [!NOTE]
   > URL は任意の URL にすることができますが、既定では、ジェネレーターは Azure Web サイトの URL を提案します。

1. 次の質問では、ソリューションの単体テストを含めるかどうかを確認します。 デフォルトの応答は *yes* です。 単体テストを含める場合、生成されたプロジェクトには、スキャフォールディングされるさまざまな項目に対して単体テスト フレームワークと既定の単体テストが含まれます。 
   > [!NOTE]
   > * このチュートリアルでは、テスト フレームワークを含めないように選択します。
   > * ジェネレーターには、オプトインまたはオプトアウトできる多くの拡張機能が組み込まれています。

1. サインインを簡単にするために、サインインに Azure アプリケーション インサイトを使用するかどうかも確認されます。 *[はい*] を選択した場合は、Azure アプリケーションの洞察キーを指定する必要があります。 

   > [!NOTE]
   > このチュートリアルでは、アプリケーションインサイトの使用をオプトアウトします。

次の質問セットは、以前に選択した項目に基づいて行われます。 タブの場合は、名前を指定するだけで、必要に応じてこのアプリをSharePointオンライン Web パーツとして使用できるようにする場合に選択します。 名前を指定すると、ジェネレータはプロジェクトを生成し、すべての依存関係をインストールします。 これには1、2分かかります。

## <a name="add-some-code-to-your-tab"></a>タブにコードを追加する

ジェネレーターが完了したら、お気に入りのコード エディターでソリューションを開くことができます。 1、2 分かかると、コードの構成方法に慣れ親しみます。 詳細については、構造体のドキュメント[Project](https://github.com/OfficeDev/generator-teams/wiki/Project-Structure)参照してください。

タブがファイル内にあります `./src/app/scripts/myFirstAppTab/MyFirstAppTab.tsx` 。 これは、タブの TypeScript React ベースのクラスです。メソッドを見つけて `render()` 、次のようにコントロール内にコード行 `<PanelBody>` を追加します。

``` TypeScript
<PanelBody>
    <div style={styles.section}>
    Hello World! Yo Teams rocks!
    </div>
</PanelBody>
```

ファイルを保存し、コマンド プロンプトに戻ります。

## <a name="build-your-app"></a>アプリを作成する

これで、プロジェクトをビルドできます。 これは 2 つのステップ (または 1 つのステップ、 以下を参照) で行われます。

まず、アップロード/サイドロードをMicrosoft TeamsするTeamsアプリマニフェストファイルを作成する必要があります。 これは Gulp タスクによって行われます `gulp manifest` 。 これにより、マニフェストが検証され、ディレクトリに zip ファイルが作成 `./package` されます。

ソリューションをビルドするには、コマンドを使用 `gulp build` します。 これにより、ソリューションがフォルダに入 `./dist` り込みます。 

## <a name="run-your-app"></a>アプリの実行

アプリを実行するには、コマンドを使用 `gulp serve` します。 これにより、アプリをテストするためのローカル Web サーバーが構築され、起動されます。 このコマンドは、プロジェクトにファイルを保存するたびにアプリケーションを再構築します。 

`http://localhost:3007/myFirstAppTab/`これで、タブがレンダリングされていることを確認するために参照できるようになります。 しかし、まだMicrosoft Teamsではありません:

![ブラウザでサイトを表示する](~/assets/yeoman-images/teams-first-app-3.png)

## <a name="run-your-app-in-microsoft-teams"></a>Microsoft Teamsでアプリを実行する

Microsoft Teamsでは、アプリを localhost でホストすることはできませんので、パブリック URL に発行するか、ngrok などのプロキシを使用する必要があります。

良いニュースは、足場のプロジェクトにはこの組み込みがあるということです。 `gulp ngrok-serve`ngrok サービスを実行すると、一意のパブリック DNS エントリを使用してバックグラウンドで開始され、その一意の URL を持つマニフェストもパッケージ化され、 とまったく同じ処理が行われます `gulp serve` 。

を実行した後 `gulp ngrok-serve` 、新しいMicrosoft Teamsチームを作成し、作成したら [チーム名] をクリックしてチームの設定に移動し、[*アプリ*] を選択します。 右下隅に *カスタム アプリアップロード* リンクが表示されます `package` 。 そのフォルダの zip ファイルを選択し、[開く] を選択します。 アプリがMicrosoft Teamsにサイドロードされました。

![サイドロードアプリ](~/assets/yeoman-images/teams-first-app-4.png)

*[全般*] チャネルに戻り、 *+* 新しいタブを追加します。タブのリストにタブが表示されます。

![[構成] タブ](~/assets/yeoman-images/teams-first-app-5.png)

タブを選択し、指示に従って追加します。 カスタム構成ダイアログがあり、ソースを編集できることに注意してください。 [ *保存]* を選択して、チャンネルにタブを追加します。 一度あなたのタブは、Microsoft Teamsの中にロードする必要があります!

![チーム内での実行中のタブ](~/assets/yeoman-images/teams-first-app-6.png)

## <a name="upgrade-microsoft-teams"></a>Microsoft Teamsのアップグレード

また、Microsoft TeamsのYeomanジェネレータを使用して、現在のMicrosoft Teamsバージョンを最新バージョンにアップグレードすることもできます。

**Microsoft Teamsをアップグレードするには**

1. 次のコマンドを使用して、Teamsの現在のバージョンを取得します。

   ```PowerShell
    yo teams --version
   ```
2. 次のコマンドを使用して、ジェネレータの更新を選択します。

   ```PowerShell
    yo
   ```
3. 矢印キーを使用して **、[ジェネレータを更新] を選択します**。

   ![ヨセレクトアップダットゲンの画像](~/assets/images/Update-Teams/YoSelectUpdateGen.png)

4. ジェネレータのリストから、必要なジェネレータを選択します。
   > [!NOTE]
   > スペースバーを使用して、選択したTeamsバージョンを選択または選択解除します。

    ![使用スペースのイメージを選択するジェネレータ](~/assets/images/Update-Teams/UseSpaceToSelectGenerators.png)
    

   > [!NOTE]
   > インストールが完了するまで数秒から数分Teamsかかります。

5. インストールが完了したら、次のコマンドを使用してインストール済みバージョンを確認します。

   ```PowerShell
    yo teams --version
   ```
   
**おめでとう！最初のMicrosoft Teams アプリを構築して展開しました。Microsoft Teamsもアップグレードしました。**
