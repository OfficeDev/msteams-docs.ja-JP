## <a name="deploy-your-app-to-azure"></a>アプリを Azure にデプロイする

デプロイは、2 つの手順で構成されます。 まず、必要なクラウド リソースが作成されます (プロビジョニングとも呼ばれます)。 次に、アプリのコードが作成されたクラウド リソースにコピーされます。 このチュートリアルでは、タブ アプリをデプロイします。
<br>
<br>
<details>
<summary>プロビジョニングとデプロイの違いは何ですか?</summary>
<br>
<b>[プロビジョニング]</b> 手順では、アプリ用に Azure と Microsoft 365 にリソースを作成しますが、コード (HTML、CSS、JavaScript など) はリソースにコピーされません。 <b>[デプロイ]</b> ステップでは、プロビジョニング 手順中に作成したリソースにアプリのコードがコピーされます。 新しいリソースをプロビジョニングせずに複数回デプロイするのが一般的です。 プロビジョニング手順の完了には時間がかかる場合があるため、デプロイ手順とは別です。
</details>
<br>

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

Visual Studio Code のサイド バーで Teams Toolkit :::image type="icon" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: アイコンを選択します。

1. **[クラウドにプロビジョニング]** を選択します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="プロビジョニング コマンドを示すスクリーンショット":::

1. 既存のサブスクリプションのすべてのユーザーを選択します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/select-subscription.png" alt-text="既存のサブスクリプションの選択を示すスクリーンショット":::

1. Azure リソースに使用するリソース グループを選択します。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/select-resource.png" alt-text="プロビジョニング用のリソースを示すスクリーンショット":::

   > [!NOTE]
   > アプリは Azure リソースを使用してホストされます。
   >
   >詳細については、「[リソース グループの作成](/azure/azure-resource-manager/management/manage-resource-groups-portal)」を参照してください。

    Azure でリソースを実行するときにコストが発生する可能性があることを示すダイアログが表示されます。

1. **[プロビジョニング]** を選択します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provision-warning.png" alt-text="ダイアログのプロビジョニングを示すスクリーンショット。":::

   :::image type="content" source="~/assets/images/teams-toolkit-v2/provision-confirm1.png" alt-text="サブスクリプションの選択を示すスクリーンショット。":::

   プロビジョニング プロセスでは、Azure クラウドにリソースが作成されます。 時間がかかる場合があります。 進行状況を監視するには、右下隅にあるダイアログを確認します。 数分後に、次の通知が表示されます。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-provision-successmsgext.png" alt-text="クラウドで正常にプロビジョニングされたリソースを示すスクリーンショット。":::

    必要に応じて、プロビジョニングされたリソースを表示できます。 このチュートリアルでは、リソースを表示する必要はありません。

    プロビジョニングされたリソースが [ **環境** ] セクションに表示されます。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/provisioned-resources-env.png" alt-text="プロビジョニングされたリソースを示すスクリーンショット。":::

1. プロビジョニングが完了したら、[デプロイ] パネルから [**クラウドに****デプロイ]** を選択します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/deploy-cloud.png" alt-text="クラウドへのデプロイを示すスクリーンショット。":::

   プロビジョニングと同様に、デプロイには時間がかかります。 プロセスを監視するには、右下隅にあるダイアログを確認します。 数分後に完了通知が表示されます。

これで、同じプロセスを使用して、ボットとメッセージ拡張機能アプリを Azure にデプロイできます。

# <a name="command-line"></a>[Command Line/コマンド ライン](#tab/cli)

ターミナル ウィンドウで以下を行います。

1. `teamsfx provision` を実行します。

   ``` bash
   teamsfx provision
   ```

   メッセージが表示されたら、Azure リソースを使用する Azure サブスクリプションを選択します。

1. `teamsfx deploy` を実行します。

   ``` bash
   teamsfx deploy
   ```

---

> [!NOTE]
> アプリは Azure リソースを使用してホストされます。

## <a name="run-the-deployed-app"></a>デプロイされたアプリを実行する

プロビジョニングとデプロイの手順が完了したら、次の手順を実行します。

1. Visual Studio Code からデバッグ パネル (**Ctrl + Shift + D** / **⌘⇧-D** または **View > Run) を** 開きます。
1. [起動構成] ドロップダウンから [ **リモートの起動 (Edge)]** を選択します。
1. [ **デバッグの開始 ] (F5)** を選択して、Azure からアプリを起動します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/launch-remote.png" alt-text="アプリをリモートで起動する方法を示すスクリーンショット。":::

1. アプリを Teams にサイドロードするように求められたら、[ **追加]** を選択します。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/remote-app-client.png" alt-text="インストールされているアプリを示すスクリーンショット。":::

    これで、最初のタブ アプリが Azure 環境で実行されています。

   :::image type="content" source="~/assets/images/teams-toolkit-v2/deploy-azure/azure-deployed-apptab.png" alt-text="今すぐまたは後でアプリを試すメッセージを示すスクリーンショット。":::
