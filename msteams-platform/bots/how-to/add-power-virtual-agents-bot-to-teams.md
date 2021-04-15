---
title: Teams に Power Virtual Agents チャットボットを追加する
author: laujan
description: Teams プラットフォームでの Power Virtual Agents チャットボットの統合
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 6103e3b58d7283eab6e9a9932f6dc7778d6fc697
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697096"
---
# <a name="integrate-a-power-virtual-agents-chatbot-with-microsoft-teams"></a>Power Virtual Agents チャットボットを Microsoft Teams に統合する

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) はコードなしガイド付きグラフィカル インターフェイス ソリューションで、チームのすべてのメンバーが Teams プラットフォームと簡単に統合できるリッチで会話型のチャットボットを作成できます。 Power Virtual Agents で作成されたコンテンツはすべて、Teams および Power Virtual Agents ボットで自然にレンダリングされ、Teams ネイティブ チャット キャンバスでユーザーと関わり合います。 IT 管理者、ビジネス アナリスト、ドメイン スペシャリスト、および熟練したアプリ開発者は、開発環境をセットアップしたり、Web サービスを作成したり、ボット フレームワークに直接登録したりすることなく、Teams のインテリジェント仮想エージェントを設計、開発、発行できます。  *「Microsoft* Power Virtual Agents [を使用して Teams 用チャットボットを作成する」を参照してください](../bot-features.md#bots-and-the-microsoft-power-virtual-agents)。

> [!NOTE]
> チャットボットを Microsoft Teams に追加すると、ボット コンテンツやエンド ユーザー チャット コンテンツなどの一部のデータが Microsoft Teams と共有されます (つまり[](/power-virtual-agents/data-location)、データは組織のコンプライアンスや地理的または地域の境界外に流れる)。 <br/>
> 詳細については [、「Microsoft Teams のセキュリティとコンプライアンス」を参照してください](/MicrosoftTeams/security-compliance-overview)。

## <a name="make-your-chatbot-available-in-teams-via-the-power-virtual-agents-portal"></a>Power Virtual Agents ポータルを介して Teams でチャットボットを利用可能にする

1. **最新のボット コンテンツを発行します**。  [Power Virtual Agents](https://powervirtualagents.microsoft.com)ポータルでチャットボットを作成した後、Teams ユーザーがボットを操作するには、少なくとも 1 回はボットを発行する必要があります。 「最新 [のボット コンテンツを発行する」を参照してください](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)。

![Power Virtual Agents ポータルで発行する](../../assets/images/pva-publish.png)

2. **Teams チャネルを構成します**。 ボットを発行した後、Teams チャネルを追加して、ボットを Teams ユーザーが利用できます。

![電源仮想エージェント ポータルのチャネル](../../assets/images/pva-channels.png)

3. **チャットボットのアプリ ID を生成します**。  Teams チャネルがチャットボットに正常に追加されると、ダイアログ ボックスに **アプリ ID** が生成されます。 アプリ ID は、ボットの Microsoft が生成した一意の識別子です。  アプリ ID をコピーして保存します。後で Teams 用のアプリ パッケージを作成する必要があります。

## <a name="add-your-bot-to-teams-using-app-studio"></a>App Studio を使用してボットを Teams に追加する

Teams [インスタンスでカスタム アプリ](/microsoftteams/admin-settings) のアップロードが有効になっている場合は、Teams App Studio を使用してチャットボットを直接アップロードし、その使用を直に開始できます。 チャットボットを共有する場合は、管理者がボットをテナント アプリ カタログで利用できるよう要求するか、他のユーザーにアプリ パッケージを送信して個別にアップロードを依頼することもできます。

1. **Teams に App Studio をインストールします**。 App Studio は Teams ストアからインストールできる Teams アプリで、Teams でのボットの作成と登録を簡略化します。 

  * Teams インスタンスの左側のナビゲーション バーの下部からアプリ ストア アイコンを選択し **、App Studio を検索します**。
>

&emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="/msteams-docs/msteams-platform/assets/images/get-started/app-studio-store.png"/>   

  * [App **Studio] タイルを** 選択し **、ポップアップ** ダイアログ ボックスで [インストール] を選択します。
>
&emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

2. **App Studio で Teams アプリ マニフェストを作成します**。  Teams のボットは、ボットとその機能に関する基本情報を提供するアプリ マニフェスト (JSON) ファイルによって定義されます。 [App **Studio] で**[マニフェスト エディター **] [**   =>  **新しいアプリを作成する] を選択します**。
3. **ボットの詳細を追加します**。 各フィールドの詳細については、「マニフェスト スキーマ定義 [」を参照してください](../../resources/schema/manifest-schema.md)。 必ずすべての必須フィールドに入力してください。
4. **ボットをセットアップします**。 [ボット] **タブに移動し** 、[セットアップ] ボタン **を** 選択し、[既存のボット] **を** 選択し、ボット名を入力します。
5. **アプリ ID を追加します**。[別の **ボット ID に接続する] に移動し** 、前にコピーした **アプリ ID** に貼り付けます。 [スコープ] で [個人用] **を選択** し、[保存] を **選択します**。
6. **ボットの有効なドメインを追加します**。  この手順は、ボットがユーザーにサインインを要求する場合にのみ必要です。 [ドメイン **とアクセス許可] に移動し、[** 有効な **ドメイン** ] フィールドに次の値を入力します。

```bash
token.botframework.com
```

7.  **ボットをテストして配布します**。 [テストと **配布] タブを選択** し、[インストール] **を選択** して、ボットを Teams インスタンスに直接追加します。 必要に応じて、完成したアプリ パッケージをダウンロードして Teams ユーザーと共有したり、管理者に提供して、テナント アプリ カタログでボットを利用することもできます。
8. **チャットを開始します**。 Power Virtual Agents チャット ボットを Teams に追加するセットアップ プロセスは完了です。 これで、個人用チャットでボットとの会話を開始できます。

> [!div class="nextstepaction"]
> [詳細: Power Virtual Agents ボットを発行する](/power-virtual-agents/publication-fundamentals-publish-channels)
