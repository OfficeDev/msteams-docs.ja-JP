### <a name="optional-adjust-your-browser-launch-settings"></a>(省略可能)ブラウザーの起動設定を調整する

アプリを開発Teams、別の開発者テナントまたは代替資格情報を使用してアプリを実行するのが一般的です。  ブラウザー Microsoft Edge Google Chrome には、ブラウザーの起動設定を調整する機能が用意されています。  たとえば、プロジェクトを更新して InPrivate モード (Microsoft Edge) をサポートするには、プロジェクトで `.vscode/launch.json` ファイルを開きます。  適切な起動設定を探し、各ブロックに次のブロックを追加します。

``` json
"runtimeArgs": [ "--inprivate" ]
```

たとえば、ローカルで実行する起動設定は次のように表示されます。

``` json
{
   "name": "Start and Attach to Frontend (Edge)",
   "type": "pwa-msedge",
   "request": "launch",
   "url": "https://teams.microsoft.com/_#/l/app/${localTeamsAppId}?installAppPackage=true",
   "preLaunchTask": "Start Frontend",
   "postDebugTask": "Stop All Services",
   "presentation": {
         "group": "all",
         "hidden": true
   },
   "runtimeArgs": [ "--inprivate" ]
},
```

または、最後の既知のプロファイルを使用するブラウザーを構成することもできます。 [新しいプロファイルを作成Microsoft Edge。](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435)  次に、新しいリンクに最後の既知のプロファイルを使用する設定を調整します。

- [Microsoft Edge] を開きます `edge://settings/profiles/multiProfileSettings` 。
- [プロファイルの **自動切り替え] をオフにします**。
- [外部リンク **の既定のプロファイル] で、[** 前回使用] **(既定) を選択します**。

アプリをデバッグする前に、ブラウザーが正しいプロファイルに開かされていることを確認します。
