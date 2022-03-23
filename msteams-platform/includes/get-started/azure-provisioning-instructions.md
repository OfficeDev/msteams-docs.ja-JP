## <a name="deploy-your-app-to-azure"></a>アプリを Azure に展開する

展開は 2 つの手順で構成されます。  まず、必要なクラウド リソースが作成されます (プロビジョニングとも呼ばれる)。 次に、アプリのコードが作成されたクラウド リソースにコピーされます。 このチュートリアルでは、タブ アプリを展開します。

> <details>
> <summary>プロビジョニングと展開の違いは何ですか?</summary>
>
> [**プロビジョニング]** 手順では、Azure とアプリの Microsoft 365 にリソースを作成しますが、コード (HTML、CSS、JavaScript など) はリソースにコピーされません。 [ **展開]** 手順では、アプリのコードをプロビジョニング 手順で作成したリソースにコピーします。 新しいリソースをプロビジョニングせずに複数回展開するのが一般的です。 プロビジョニング 手順の完了には時間がかかる場合があります。展開手順とは別の手順です。
</details>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

Visual Studio Code のサイド バーで Teams Toolkit :::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: アイコンを選択します。

1. [クラウド **でプロビジョニング] を選択します**。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="プロビジョニング コマンドを示すスクリーンショット" border="false":::

1. Azure リソースに使用するサブスクリプションを選択します。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="プロビジョニングのリソースを示すスクリーンショット" border="false":::

   > [!NOTE]
   > アプリのホスティングに使用される Azure リソースは常にいくつかある。

    Azure でリソースを実行するときにコストが発生する可能性があるという警告がダイアログで表示されます。

1. [プロビジョニング **] を選択します**。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="プロビジョニング ダイアログのスクリーンショット。" border="false":::

   プロビジョニング プロセスによって、Azure クラウドにリソースが作成されます。 時間がかかる場合があります。 右下隅のダイアログを見て、進行状況を監視できます。 数分後、次の通知が表示されます。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-success.png" alt-text="プロビジョニング完了ダイアログを示すスクリーンショット。" border="false":::

    必要な場合は、プロビジョニングされたリソースを表示できます。 このチュートリアルでは、リソースを表示する必要があります。

    プロビジョニングされたリソースが [環境] セクション **に表示** されます。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="プロビジョニング完了ダイアログを示すスクリーンショット。" border="false":::

1. プロビジョニング **が完了したら、[展開]** パネル **から** [クラウドへの展開] を選択します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="クラウドに展開する場所を示すスクリーンショット。" border="false":::

   プロビジョニングと同様に、展開には時間がかかる場合があります。 右下隅のダイアログを見て、プロセスを監視できます。 数分後、完了通知が表示されます。

これで、同じプロセスを使用してボットアプリとメッセージ拡張機能アプリを Azure に展開できます。

# <a name="command-line"></a>[Command Line/コマンド ライン](#tab/cli)

ターミナル ウィンドウで次の設定を行います。

1. `teamsfx provision` を実行します。

   ``` bash
   teamsfx provision
   ```

   メッセージが表示されたら、Azure リソースを使用する Azure サブスクリプションを選択します。

   > [!NOTE]
   > アプリのホスティングに使用される Azure リソースは常にいくつかある。

1. `teamsfx deploy` を実行します。

   ``` bash
   teamsfx deploy
   ```

---

## <a name="run-the-deployed-app"></a>展開されたアプリを実行する

プロビジョニングと展開の手順が完了したら、次の手順を実行します。

1. [デバッグ] パネル (**Ctrl + Shift + D** / **??-D** または View **>実行**) を開Visual Studio Code。
1. [起動 **構成] ドロップダウンから [リモートの起動 ] (エッジ)** を選択します。
1. [再生] ボタンを選択して、Azure からアプリを起動します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="起動アプリをリモートで示すスクリーンショット。" border="false":::

1. **[追加]** を選択します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/remote-app-client.png" alt-text="インストールされているアプリを示すスクリーンショット。" border="false":::

   アプリが Azure サイトに読み込まれます。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/azure-deployed-app.png" alt-text="インストールされているアプリを示すスクリーンショット。" border="false":::

    おめでとうございます! これで、タブ アプリは Azure からリモートで実行されています。
