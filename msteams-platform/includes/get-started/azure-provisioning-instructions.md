## <a name="deploy-your-app-to-azure"></a>アプリを Azure に展開する

展開は 2 つの手順で構成されます。  まず、必要なクラウド リソース (プロビジョニングとも呼ばれる) が作成され、アプリを構成するコードが作成されたクラウド リソースにコピーされます。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Visual Studio Code を開きます。
1. サイドバーからTeams Toolkitアイコンを選択してTeamsします。
1. [クラウド **でプロビジョニング] を選択します**。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="プロビジョニング コマンドを示すスクリーンショット":::

1. 必要に応じて、Azure リソースに使用するサブスクリプションを選択します。

   > [!NOTE]
   > アプリのホスティングに使用される Azure リソースは常にいくつかある。

1. Azure でリソースを実行するときにコストが発生する可能性があるという警告がダイアログで表示されます。  [プロビジョニング **] を押します**。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-warning.png" alt-text="プロビジョニング ダイアログのスクリーンショット。":::

   プロビジョニング プロセスによって、Azure クラウドにリソースが作成されます。  これには時間がかかるでしょう。  右下隅のダイアログを見て、進行状況を監視できます。  数分後、次の通知が表示されます。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-complete.png" alt-text="プロビジョニング完了ダイアログを示すスクリーンショット。":::

1. プロビジョニングが完了したら、[クラウドに **展開する] を選択します**。  プロビジョニングと同様に、このプロセスには時間がかかる場合があります。  右下隅にあるダイアログを見て、プロセスを監視できます。 数分後、完了通知が表示されます。

# <a name="command-line"></a>[Command Line/コマンド ライン](#tab/cli)

ターミナル ウィンドウで次の設定を行います。

1. `teamsfx provision` を実行します。

   ``` bash
   teamsfx provision
   ```

   Azure サブスクリプションにログインするように求めるメッセージが表示される場合があります。  必要に応じて、Azure リソースに使用する Azure サブスクリプションを選択するように求めるメッセージが表示されます。

   > [!NOTE]
   > アプリのホスティングに使用される Azure リソースは常にいくつかある。

1. `teamsfx deploy` を実行します。

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> **プロビジョニングと展開の違いは何ですか?**
>
> プロビジョニング **手順** では、アプリの Azure と M365 にリソースが作成されますが、コード (HTML、CSS、JavaScript など) はリソースにコピーされません。  [ **展開]** 手順では、プロビジョニング 手順で作成したリソースにアプリのコードをコピーします。  新しいリソースをプロビジョニングせずに複数回展開するのが一般的です。 プロビジョニング 手順の完了には時間がかかる場合があります。展開手順とは別の手順です。

プロビジョニングと展開の手順が完了したら、次の手順を実行します。

1. [Visual Studio Codeから、デバッグ パネルを開きます **(Ctrl+Shift+D**  /  **[ctrl]+[--D]** または [実行>**表示**)
1. [起動 **構成] ドロップダウンから [リモート** の起動 ] (エッジ) を選択します。
1. [再生] ボタンを押してアプリを起動します 。Azure からリモートで実行中です。
