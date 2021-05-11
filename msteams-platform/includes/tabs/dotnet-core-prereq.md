## <a name="prerequisites"></a>前提条件

- このクイック スタートを完了するには、カスタム アプリのアップロードMicrosoft 365許可を有効にしたテナントとチーム *が必要* です。 詳細については、「Prepare [your Microsoft 365 テナント」を参照してください](~/concepts/build-and-test/prepare-your-o365-tenant.md)。
  - 現在アカウントをお持ちMicrosoft 365場合は、Microsoft Developer Program を通じて無料サブスクリプションに[サインアップできます](https://developer.microsoft.com/en-us/microsoft-365/dev-program)。 サブスクリプションは、継続的な開発に使用している限りアクティブなままです。

- App Studio を使用して、アプリケーションをアプリケーションにインポートTeams。 App Studio をインストール **するには、アプリ** アプリの左下隅にある [アプリ ストア アプリ] を選択Teams App Studio ![ ](~/assets/images/tab-images/storeApp.png) を検索します。 タイルを見つけたら、タイルを選択し、ポップアップ ウィンドウ ダイアログ ボックスで [インストール] を選択します。

さらに、このプロジェクトでは、次のコードが開発環境にインストールされている必要があります。

- .NET CORE クロスVisual Studioワークロードがインストールされている IDE の現在 **の** バージョン。 まだインストールされていない場合はVisual Studio最新のバージョンを無料で[Microsoft Visual Studio Communityインストールできます](https://visualstudio.microsoft.com/downloads)。

- [ngrok](https://ngrok.com)リバース プロキシ ツール。 ngrok を使用して、ローカルで実行している Web サーバーのパブリックに利用可能な HTTPS エンドポイントへのトンネルを作成します。 こちらから [ダウンロードできます](https://ngrok.com/download)。
