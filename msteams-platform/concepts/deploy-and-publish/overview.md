---
title: アプリを配布する
description: アプリを配布するための 3 つのオプションについて説明します
ms.topic: conceptual
keywords: Teams、公開、ストア、Office、配布、AppSource、サイドロード、アップロード、アプリ
ms.openlocfilehash: 9c457608711bc491aeb9062a8ac2de58e78a90bd
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014188"
---
# <a name="distribute-your-microsoft-teams-app"></a>Microsoft Teams アプリを配布する

アプリを作成したら、次の 3 つの方法でアプリを配布できます。

1. [アプリを直接アップロードする](#upload-your-app-directly)。
2. [アプリを組織のアプリ カタログに公開する](#publish-to-your-organizations-app-catalog)。
3. [AppSource を使用してアプリを公開する](#publish-to-appsource)。

## <a name="enterprise-organizations"></a>エンタープライズ組織

### <a name="upload-your-app-directly"></a>アプリを直接アップロードする

これは、アプリをテストおよび使用する最も簡単な方法です。 チームの所有者である場合や、[カスタム アプリのアップロードが有効](/microsoftteams/admin-settings)になっている場合は、アプリを[直接アップロード (またはサイドロード)](./apps-upload.md) して、すぐに使用を開始することができます。 ただし、アプリを他のユーザーと共有する場合は、アプリ パッケージを送信して、個別にアップロードするように依頼する必要があります。

アプリを幅広く配布する場合は、ユーザーは Teams のアプリ内のギャラリーを利用して、高品質の Teams のアプリを見つけることができます。 ギャラリーでソリューションを使用するには、組織のアプリ カタログ[](#publish-to-your-organizations-app-catalog)に発行するか、AppSource に発行[する必要があります](./appsource/publish.md)。

### <a name="publish-to-your-organizations-app-catalog"></a>組織のアプリ カタログへの公開

組織のアプリ カタログには、組織固有のアプリが含まれており、そのアプリの制御は組織が行います。 詳細については、「[*アプリを組織のアプリ カタログに公開する*](/microsoftteams/tenant-apps-catalog-teams)」の記事を参照してください。 この機能は、Microsoft Office 365 テナントの管理者特権を持つ Teams ユーザーのみが管理できます。

### <a name="publish-to-appsource"></a>AppSource への公開

AppSource (旧称 Office ストア) は、Office アドインや SharePoint アドインなど、他の Office 365 の拡張機能だけでなく、Microsoft Teams アプリの配布場所としても有効活用できます。[AppSource にアプリを送信](./appsource/publish.md)するには、ガイドラインに従ってください。

## <a name="government-community-cloud-gcc-organizations"></a>政府機関コミュニティ クラウド (GCC) 組織

### <a name="upload-your-custom-app-directly-to-teams"></a>カスタム アプリを Teams に直接アップロードする

 GCC テナント管理者は、カスタム アプリをテナント環境にアップロードするかどうか、およびそれをテナント アプリ カタログに公開するかどうかを決定します。 Microsoft はカスタム アプリケーションを所有または制御していないので、すべてのエンドポイントが組織の要件に準拠していることを確認する必要があります。 さらに、アプリ ソリューションにボットまたはメッセージ拡張機能が含まれる場合は、次のように Bot [Framework](https://dev.botframework.com/) の登録を完了する必要があります。

1. [チャネル **への接続] ページの** [ **注目のチャネル** の追加] で **、[Teams]** を選択します。
1. **[MSTeams の構成] ページに移動** します (*下記を* 参照)。
1. [ **メッセージング] で、** 政府機関向け **Microsoft Teams の [顧客向け] ラジオ ボタン** を選択します。
1. ページの左下隅で、[保存] を選択 **します**。  

>[!IMPORTANT]
> Teams の商用構成を使用してカスタム アプリを GCC 環境にアップロード/サイドロードすることはできません。GCC 準拠の構成には、政府機関向け **Microsoft Teams for Customers** ラジオ ボタンを選択する必要があります。

![Teams のメッセージング構成ページ](../../assets/images/gcc-configure.png)

> [!NOTE]
>
> * 上記の GCC 環境のアップロード手順は、Teams カスタム アプリに適用されます。 </br>
> * 準拠している Microsoft アプリは、既定で Teams の GCC 環境で有効になっています。
> * サード パーティ製アプリはテナント レベルで無効になり、組織のアプリアクセス許可ポリシーを使用 [して管理する必要があります](/microsoftteams/teams-app-permission-policies)。 すべてのサード パーティ製アプリが組織のポリシーと手順と一致しているか確認してください。

> [!TIP]
>
> Microsoft 365 開発者パートナーは [、Microsoft 365](/microsoft-365-app-certification/overview)アプリ認定プログラムを通じて、サード パーティ製の Teams アプリのセキュリティ、データ処理、コンプライアンスの詳細を提供します。 *「Microsoft* [Teams アプリ認定」も参照してください](/microsoftteams/platform/concepts/deploy-and-publish/appsource/post-publish/application-certification)。
</br></br>
