---
title: チャットボットPower Virtual Agents Teamsに追加する
author: laujan
description: Teams プラットフォームにPower Virtual Agentsチャットボットを統合する
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 2a8f9c23eaa1acf2555b91cc4caf8d0f3298c114
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566118"
---
# <a name="add-power-virtual-agents-chatbot"></a>Power Virtual Agents チャットボットを追加する 

Power Virtual Agentsは、Teamsプラットフォームと簡単に統合できる豊富な会話型チャットボットを作成できる、コードなしのガイド付きグラフィカルインターフェイスソリューションです。 Power Virtual Agentsで作成されたすべてのコンテンツは、Teamsで自然にレンダリングされます。 Power Virtual Agentsボットは、Teamsネイティブチャットキャンバスでユーザーと交流します。 IT 管理者、ビジネス アナリスト、ドメイン スペシャリスト、および熟練したアプリ開発者は、開発環境をセットアップしなくても、Teams用のインテリジェント仮想エージェントを設計、開発、および公開できます。 Web サービスを作成することも、Bot フレームワークに直接登録することもできます。 

このドキュメントでは、Power Virtual Agents ポータルを通じてチャットボットをTeamsで利用できるようにする方法と、App Studio を使用してボットをTeamsに追加する方法について説明します。 

Power Virtual Agentsを使用すると、顧客、他の従業員、またはウェブサイトやサービスへの訪問者が提起した質問に答えることができる強力なチャットボットを作成できます。

これらのボットは、データ サイエンティストや開発者が必要とせずに簡単に作成できます。

> [!NOTE]
> Microsoft Teamsにチャットボットを追加すると、ボット コンテンツやユーザー チャット コンテンツなどの一部のデータがMicrosoft Teamsと共有されます。 つまり、データは [組織のコンプライアンスや地理的または地域の境界](/power-virtual-agents/data-location)の外に流れます。 <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a>Power Virtual Agents ポータルを介してチャットボットをTeamsで利用できるようにする

Power Virtual Agents ポータルを通じてチャットボットをTeamsで利用できるようにするには、次のプロセス手順を実行する必要があります。

**チャットボットをTeamsで利用できるようにするには**

1. **最新のボット コンテンツを発行する**  
Power Virtual Agents ポータルでチャットボットを作成した後、ユーザーが操作できるようにするには、Teams前にボットを公開する必要があります。 詳細については、「 [最新のボット コンテンツを発行する](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)」を参照してください。

   ![電源仮想エージェント ポータルでの公開](../../assets/images/pva-publish.png)

1. **Teams チャネルを構成する**  
ボットを公開したら、Teamsチャネルを追加して、ボットをTeamsユーザーが利用できるようにします。

   ![電源仮想エージェント ポータルのチャネル](../../assets/images/pva-channels.png)

1. **チャットボットのアプリ ID を生成する**  
チャットボットにTeamsチャンネルを追加すると、ダイアログボックスに **アプリID** が生成されます。 アプリ ID は、マイクロソフトが生成したボットの一意の識別子です。 アプリ ID を保存して、Teams用のアプリ パッケージを作成します。

## <a name="add-your-bot-to-teams-using-app-studio"></a>アプリスタジオを使用してTeamsにボットを追加する

Teamsインスタンスで[カスタムアプリのアップロードが有効になっている場合、Teams](/microsoftteams/admin-settings) App Studio を使用してチャットボットを直接アップロードし、すぐに使用を開始できます。 チャットボットを共有するには、管理者にリクエストして、ボットをテナント アプリ カタログで利用できるようにするか、アプリ パッケージを他のユーザーに送信して、個別にアップロードするように依頼することができます。

1. **Teams に App Studio をインストールする**  
アプリスタジオはTeamsアプリです。 Teamsでのボットの作成と登録のプロセスを簡略化するTeamsストアからアプリスタジオをインストールします。 

   1. インスタンスからアプリストアアイコンTeams選択し **、App Studio を** 検索します。

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. **[App Studio]** タイルを選択し、ポップアップ ダイアログ ボックスで [**インストール**] を選択します。

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. **アプリスタジオでTeamsアプリマニフェストを作成する**  
Teamsのボットは、ボットとその機能に関する基本情報を提供するアプリ マニフェスト JSON ファイルによって定義されます。 **[App Studio]** で [**マニフェスト エディター**] を選択し、[**新しいアプリの作成**] を選択します。

    ![新しいアプリを作成する](../../assets/images/get-started/create-new-app.png)

1. **ボットの詳細を追加する**  
すべての必須フィールドに入力します。 各フィールドの詳細については、「マニフェスト [スキーマ](../../resources/schema/manifest-schema.md)定義」を参照してください。

    ![アプリの詳細を追加する](../../assets/images/get-started/add-app-details.png)

1. **ボットを設定する** ボットをセットアップするには、次の手順に従います。 
     1. **[ボット**] タブを開きます。 
     1. [  >  **既存のボットの** セットアップ] を選択し、ボットの名前を入力します。

   ![ボットのセットアップ](../../assets/images/get-started/bot-set-up.png) 

   次の図は、既存のボットを設定する方法を示しています。      

   ![既存のボットのセットアップ](../../assets/images/get-started/existing-bot-set-up.png)
       
1. **アプリ ID を追加する**  
アプリ ID を追加するには、次の手順を実行します。  
    1. **[Connect別のボット ID に** 選択し、先ほどコピーした **アプリ ID** を貼り付けます。 
    1. **[ スコープ**  >  **の個人用**  >  保存 ]**を選択** します。

    ![アプリ ID を追加する](../../assets/images/get-started/add-app-id.png)

1. **ボットの有効なドメインを追加する**  
この手順は、ボットでユーザーがサインインする必要がある場合にのみ必要です。 [ **ドメインとアクセス許可] を** 選択し、[ **有効なドメイン]** フィールドに次の入力を入力します。

    ```bash
       token.botframework.com
    ```

1. **ボットをテストして配布する**  
**[テストと配布**] タブを開き、[**インストール]** を選択して、ボットをTeamsインスタンスに直接追加します。 または、完成したアプリ パッケージをダウンロードしてTeamsユーザーと共有したり、管理者に提供してボットをテナント アプリ カタログで利用できるようにしたりできます。

1. **チャットを開始する**   
Power Virtual AgentsチャットボットをTeamsに追加するためのセットアッププロセスが完了しました。 これで、個人的なチャットでボットとの会話を開始できるようになりました。

## <a name="see-also"></a>関連項目

- [Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  

- [マイクロソフト Power Virtual Agents でTeamsするためのチャット ボットを作成](../bot-features.md#bots-and-the-microsoft-power-virtual-agents)します。  

- [Power Virtual Agentsポータル](https://powervirtualagents.microsoft.com)

- [Power Virtual Agentsボットを公開する](/power-virtual-agents/publication-fundamentals-publish-channels)

- [Microsoft Teams のセキュリティとコンプライアンス](/MicrosoftTeams/security-compliance-overview)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [仮想アシスタントの作成](~/samples/virtual-assistant.md)

