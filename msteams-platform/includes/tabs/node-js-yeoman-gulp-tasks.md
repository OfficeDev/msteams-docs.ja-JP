## <a name="create-the-app-package"></a>アプリパッケージを作成する

Teams でタブをテストするには、アプリパッケージが必要になります。 これは、次の必要なファイルが含まれる zip フォルダーです。

- 192 x 192 ピクセルを測定する**フルカラーアイコン**。
- 32 x 32 ピクセルを測定する**透明のアウトラインアイコン**。
- アプリの属性を指定する**manifest.xml**ファイル。

パッケージは、gulp タスクを使用して作成され、マニフェストファイルを検証し、 `./package directory`で zip フォルダーを生成します。 コマンドプロンプトで、次のように入力します。

```bash
gulp manifest
```

## <a name="build-your-application"></a>アプリケーションをビルドする

Build コマンドは、ソリューションを*transpiles フォルダーに組み込みます。* 次に、次のように入力します。

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a>Localhost でアプリケーションを実行する

次のように入力して、ローカル web サーバーを起動します。

```bash
gulp serve
```

ブラウザー `http://localhost:3007/<yourDefaultAppNameTab>/`に Enter キーを押して、アプリケーションのホームページを表示します。

![ホームページのスクリーンショット](~/assets/images/tab-images/homePage.png)