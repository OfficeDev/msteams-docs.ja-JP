---
title: Power Virtual Agents chatbot を Teams に追加する
author: laujan
description: Teams プラットフォームでの Power Virtual Agent chatbot の統合
ms.topic: how-to
ms.author: lajanuar
ms.openlocfilehash: 57b06fd0d3e1fae0cbfb927335fb1b5941396bb0
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434525"
---
# <a name="integrate-a-power-virtual-agents-chatbot-with-microsoft-teams"></a>Power Virtual Agents chatbot を Microsoft Teams と統合する

[パワー仮想エージェント](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)は、コードを使用しないグラフィカルインターフェイスソリューションであり、チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できる多彩な会話を作成することを可能にします。 Power Virtual Agent で作成されたすべてのコンテンツは、teams とパワー仮想エージェントの場合、Teams ネイティブチャットキャンバスでユーザーと連携して表示されます。 IT 管理者、ビジネスアナリスト、ドメインスペシャリスト、および熟練したアプリ開発者は、開発環境をセットアップしたり、web サービスを作成したり、Bot フレームワークに直接登録したりしなくても、チームのためのインテリジェントな仮想エージェントを設計、開発、および発行することができます。  「 [Microsoft Power Virtual エージェントを使用して Teams の chatbot を作成する](../what-are-bots.md#create-a-chatbot-for-teams-with-microsoft-power-virtual-agents) *」を参照してください*。

> [!NOTE]
> お客様の chatbot を Microsoft Teams に追加することによって、bot コンテンツやエンドユーザーチャットコンテンツなどの一部のデータが Microsoft Teams と共有されます (つまり、データは[組織のコンプライアンスと地理的または地域の境界](/power-virtual-agents/data-location)の外部に流れます)。 <br/>
> 詳細については、「 [Microsoft Teams のセキュリティとコンプライアンス](/MicrosoftTeams/security-compliance-overview)」を参照してください。

## <a name="make-your-chatbot-reachable-in-teams-in-the-power-virtual-agents-portal"></a>Power Virtual Agents ポータルの Teams で chatbot にアクセスできるようにする

1. **最新の bot コンテンツを公開**します。  [Power Virtual Agents ポータル](https://powervirtualagents.microsoft.com)で chatbot を作成した後、Teams を少なくとも1回発行して Teams ユーザーが操作できるようにする必要があります。 「[最新の bot コンテンツを発行する](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)」を参照してください。

![パワー仮想エージェントポータルでの発行](../../assets/images/pva-publish.png)

2. **Teams チャネルを構成**します。 Bot を発行した後、teams チャネルを追加して Teams ユーザーにアクセスできるようにすることができます。

![電源仮想エージェントポータルのチャネル](../../assets/images/pva-channels.png)

3. **Chatbot のアプリ Id を生成**する Teams のチャネルが chatbot に正常に追加されると、ダイアログボックスに**アプリ Id**が生成されます。 アプリ Id は、ボットに対して一意の Microsoft 生成された識別子です。  アプリ Id をコピーして保存する-Teams 用のアプリパッケージを作成するには、後で必要になります。

## <a name="add-your-bot-to-teams-using-app-studio"></a>アプリ Studio を使用して bot を Teams に追加する

Teams インスタンスで[カスタムアプリのアップロードが有効になっ](/microsoftteams/admin-settings)ている場合は、Teams アプリ Studio を使用して、chatbot を直接アップロードし、すぐに使用を開始することができます。 Chatbot を共有する場合は、管理者がテナントのアプリカタログで bot を利用できるようにするか、他のアプリパッケージを送信して個別にアップロードするように依頼することができます。

1. **Teams にアプリ Studio をインストール**します。 App Studio は teams ストアからインストールできる Teams アプリであり、Teams でのボットの作成と登録を簡単にします。 

  * Teams インスタンスの左側のナビゲーションバーの下部にある [app store] アイコンを選択し、**アプリ Studio**を検索します。
>
&emsp;&emsp; <img  width="450px" title="ストア内のアプリ Studio の検索" src="../../assets/images/get-started/app-studio-store.png"/>    

  * [ **App Studio** ] タイルを選択し、ポップアップダイアログボックスの [**インストール**] を選択します。
>
&emsp;&emsp; <img  width="450px" title="App Studio をインストールする" src="../../assets/images/get-started/app-studio-install.png"/>

2. **App Studio で Teams アプリマニフェストを作成**します。  Teams のボットは、ボットとその機能に関する基本的な情報を提供するアプリマニフェスト (JSON) ファイルによって定義されます。 **アプリ Studio**で [**マニフェストエディター**] を選択して   =>  **、新しいアプリを作成**します。
3. **Bot の詳細を追加**します。 各フィールドの詳細については、「[マニフェストスキーマ定義](../../resources/schema/manifest-schema.md)」を参照してください。 すべての必須フィールドに入力してください。
4. **Bot をセットアップ**します。 [**ボット**] タブに移動して、[**セットアップ**] ボタンを選択し、[**既存のボット**] を選択して、bot 名を入力します。
5. **アプリ Id を追加**します。**別の bot id に接続**して、先ほどコピーした**アプリ id**に貼り付けます。 [範囲] で [**個人**] を選択し、[**保存**] を選択します。
6. **Bot の有効なドメインを追加**します。  この手順は、bot がサインインすることをユーザーに要求する場合にのみ必要です。 [**ドメインとアクセス許可**] に移動し、[**有効なドメイン**] フィールドに次を入力します。

```bash
token.botframework.com
```

7.  **Bot をテストして配布**します。 [**テストと配布**] タブを選択し、[**インストール**] を選択して、自分の Teams インスタンスに bot を直接追加します。 必要に応じて、完成したアプリパッケージをダウンロードして Teams ユーザーと共有するか、管理者に提供して、テナントのアプリカタログで bot を使用できるようにすることができます。
8. **チャットを開始**します。 Power Virtual Agents チャットボットを Teams に追加するためのセットアッププロセスは完了しています。 これで、個人のチャットで bot との会話を開始できるようになります。

> [!div class="nextstepaction"]
> [Power Virtual Agents bot の公開の詳細情報](/power-virtual-agents/publication-fundamentals-publish-channels)
