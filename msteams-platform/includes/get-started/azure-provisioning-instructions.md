## <a name="deploy-your-app-to-azure"></a>アプリを Azure にデプロイする

デプロイは 2 つの手順で構成されます。  まず、必要なクラウド リソースが作成されます (プロビジョニングとも呼ばれます)。 その後、アプリのコードが作成されたクラウド リソースにコピーされます。 このチュートリアルでは、タブ アプリをデプロイします。
<br> 
<br>
<details>
<summary>プロビジョニングとデプロイの違いは何ですか?</summary>
<br>
<b>プロビジョニング</b>手順では、アプリの Azure と Microsoft 365 にリソースが作成されますが、コード (HTML、CSS、JavaScript など) はリソースにコピーされません。 <b>[デプロイ]</b> ステップでは、プロビジョニング 手順中に作成したリソースにアプリのコードをコピーします。 新しいリソースをプロビジョニングせずに複数回デプロイするのが一般的です。 プロビジョニング手順は完了するまでに時間がかかる可能性があるため、デプロイ手順とは別です。
</details>
<br>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

Visual Studio Code のサイド バーで Teams Toolkit :::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: アイコンを選択します。

1. **[クラウドにプロビジョニング]** を選択します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="プロビジョニング コマンドを示すスクリーンショット" border="false":::

1. Azure リソースに使用するサブスクリプションを選択します。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="プロビジョニング用のリソースを示すスクリーンショット" border="false":::

   > [!NOTE]
   > アプリをホストするために使用される Azure リソースは常にあります。

    ダイアログでは、Azure でリソースを実行するときにコストが発生する可能性があることを警告します。

1. [ **プロビジョニング**] を選択します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="プロビジョニング ダイアログのスクリーンショット。" border="true":::

   プロビジョニング プロセスによって、Azure クラウドにリソースが作成されます。 時間がかかる場合があります。 右下隅にあるダイアログを見て、進行状況を監視できます。 数分後、次の通知が表示されます。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-successmsgext.png" alt-text="プロビジョニング完了のダイアログを示すスクリーンショット。" border="false":::

    必要に応じて、プロビジョニングされたリソースを表示できます。 このチュートリアルでは、リソースを表示する必要はありません。

    プロビジョニングされたリソースが **[環境** ] セクションに表示されます。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="プロビジョニング完了のダイアログを示すスクリーンショット。" border="false":::

1. プロビジョニングが完了したら、[**デプロイ]** パネルから [**クラウドにデプロイ**] を選択します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="クリックしてクラウドにデプロイする場所を示すスクリーンショット。" border="false":::

   プロビジョニングと同様に、デプロイには時間がかかります。 プロセスを監視するには、右下隅にあるダイアログを確認します。 数分後、完了通知が表示されます。

これで、同じプロセスを使用して、ボットアプリとメッセージ拡張機能アプリを Azure にデプロイできます。

# <a name="command-line"></a>[Command Line/コマンド ライン](#tab/cli)

ターミナル ウィンドウで以下を行います。

1. `teamsfx provision` を実行します。

   ``` bash
   teamsfx provision
   ```

   メッセージが表示されたら、Azure リソースを使用する Azure サブスクリプションを選択します。

   > [!NOTE]
   > アプリをホストするために使用される Azure リソースは常にあります。

1. `teamsfx deploy` を実行します。

   ``` bash
   teamsfx deploy
   ```

---

## <a name="run-the-deployed-app"></a>デプロイされたアプリを実行する

プロビジョニングとデプロイの手順が完了したら、次の手順を実行します。

1. Visual Studio Code からデバッグ パネル (**Ctrl + Shift + D** / **⌘⇧-D** または **View > Run**) を開きます。
1. 起動構成ドロップダウンから [ **Launch Remote (Edge)]** を選択します。
1. **デバッグの開始 (F5)** を選択して、Azure からアプリを起動します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="起動アプリをリモートで示すスクリーンショット。" border="false":::

1. **[追加]** を選択します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/add-mex-app.png" alt-text="インストールされているアプリを示すスクリーンショット。" border="false":::

   Toolkit には、アプリが Teams に追加されることを示すメッセージが表示されます。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/mex-added-msg.png" alt-text="スクリーンショットは、アプリを今すぐまたは後で試すためのメッセージを示しています" border="true":::
 
    - **[OK]** を選択した場合、サイドロードされたアプリの一覧から後でアプリを試すことができます。
    - **[試してみる]** を選択した場合、Teams によってアプリが読み込まれます。

   アプリは Azure サイトに読み込まれます。
   
1. **[試してみる]** を選択します。

   メッセージ拡張機能アプリが、チャット ボット アプリに読み込まれます。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/app-added-mex1.png" alt-text="Teams にサイドロードされたアプリを示すスクリーンショット" border="false":::





