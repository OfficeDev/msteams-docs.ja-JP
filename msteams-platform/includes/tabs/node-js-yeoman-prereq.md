## <a name="prerequisites"></a>前提条件

- このクイック スタートを完了するには、365 テナントOffice、カスタム アプリのアップロードを許可するを有効にしたチーム *が必要* です。 詳細については、「Prepare [your Office 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

  - 現在 365 アカウントをお持ちOffice場合は、Office 365 開発者プログラムを通じて無料サブスクリプションにサインアップできます。 サブスクリプションは、継続的な開発に使用している限りアクティブなままです。 「Welcome [to the Office 365 Developer Program」を参照してください](https://docs.microsoft.com/office/developer-program/microsoft-365-developer-program)。

さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。

- 任意のテキスト エディターまたは IDE。 コードを無料でインストール [Visual Studio使用](https://code.visualstudio.com/download) できます。

- [Node.js/npm](https://nodejs.org/en/). 最新の LTS バージョンを使用する必要があります。 ノード ノード パッケージ マネージャー (npm) は、インストール時にシステムにインストールNode.js。

- インストールが正常に完了したらNode.jsに次のように入力して [、Yeoman](https://yeoman.io/) パッケージと [gulp-cli](https://www.npmjs.com/package/gulp-cli) パッケージをインストールします。

```bash
npm install yo gulp-cli --global
```

- コマンド プロンプトに次のように入力して、Microsoft Teams Apps ジェネレーターをインストールします。

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a>プロジェクトを生成する

- コマンド プロンプトを開き、タブ プロジェクトの新しいディレクトリを作成します。

- ジェネレーターを起動するには、新しいディレクトリに移動し、次のコマンドを入力します。

```bash
yo teams
```

- 次に、アプリケーションのファイルで使用される一連の値manifest.js **します** 。

![ジェネレーターの開くスクリーンショット](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

**ソリューション名は何ですか?**

これはプロジェクト名です。 Enter キーを押すと、候補の名前を受け入れできます。

**ファイルをどこに保存しますか?**

現在、プロジェクト ディレクトリにいます。 Enter キーを押します。

**Microsoft Teams アプリ プロジェクトのタイトル**

これはアプリ パッケージ名であり、アプリ マニフェストと説明で使用されます。

**(会社) の名前(最大 32 文字)**

会社名はアプリ マニフェストで使用されます。

<br>**どのマニフェスト バージョンを使用しますか?**

既定のスキーマを選択します。

**クイック スキャフォールディング(Y/n)**

既定値は yes です。 **n と入力** して Microsoft パートナー ID を入力します。

**Microsoft パートナー ID をお持ちの場合は、Microsoft パートナー ID を入力してください。(スキップする場合は空白のままにする)**

このフィールドは必須ではありません。既に Microsoft パートナー ネットワークに参加している場合にのみ [使用してください](https://partner.microsoft.com)。

**プロジェクトに何を追加しますか?**

[( &ast; ) ] タブを選択します。

**このソリューションをホストする URL**

既定では、ジェネレーターは Azure Web サイトの URL を提案します。 アプリをローカルでテストするだけなので、このクイック スタートを完了するために有効な URL は必要ありません。

**テスト フレームワークと初期テストを含めるには?(y/N)**

この **プロジェクトの** テスト フレームワークを含めないを選択します。 既定値は yes です。 **n と入力します**。

**テレメトリに Azure Applications Insights を使用しますか?(y/N)**

Azure **Application** [Insights を含めないを選択します](/azure-docs/articles/azure-monitor/app/app-insights-overview.md)。 既定値は no です。 **n と入力します**。

**既定のタブ名 (最大 16 文字)?**

タブの名前を指定します。このタブ名は、ファイル/URL パス コンポーネントとしてプロジェクト全体で使用されます。
