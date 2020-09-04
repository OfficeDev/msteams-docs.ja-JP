---
title: アプリを配布する
description: アプリを配布するための 3 つのオプションについて説明します
keywords: Teams、公開、ストア、Office、配布、AppSource、サイドロード、アップロード、アプリ
ms.openlocfilehash: d3fd81e69f74b6332d9033412a7b6688239cd801
ms.sourcegitcommit: 02ab2cb7820dc8665bb4ec6a1a40c3b8b8f29d66
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2020
ms.locfileid: "47340961"
---
# <a name="distribute-your-microsoft-teams-app"></a>Microsoft Teams アプリを配布する

アプリを作成したら、次の 3 つの方法でアプリを配布できます。

1. [アプリを直接アップロードする](#upload-your-app-directly)。
2. [アプリを組織のアプリ カタログに公開する](#publish-to-your-organizations-app-catalog)。
3. [AppSource を使用してアプリを公開する](#publish-to-appsource)。

## <a name="enterprise-organizations"></a>エンタープライズ組織

### <a name="upload-your-app-directly"></a>アプリを直接アップロードする

これは、アプリをテストおよび使用する最も簡単な方法です。 チームの所有者である場合や、[カスタム アプリのアップロードが有効](/microsoftteams/admin-settings)になっている場合は、アプリを[直接アップロード (またはサイドロード)](./apps-upload.md) して、すぐに使用を開始することができます。 ただし、アプリを他のユーザーと共有する場合は、アプリ パッケージを送信して、個別にアップロードするように依頼する必要があります。

アプリを幅広く配布する場合は、ユーザーは Teams のアプリ内のギャラリーを利用して、高品質の Teams のアプリを見つけることができます。 ソリューションをギャラリーで使用できるようにするには、 [組織のアプリカタログに発行](#publish-to-your-organizations-app-catalog) するか、 [appsource に発行](./appsource/publish.md)する必要があります。

### <a name="publish-to-your-organizations-app-catalog"></a>組織のアプリ カタログへの公開

組織のアプリ カタログには、組織固有のアプリが含まれており、そのアプリの制御は組織が行います。 詳細については、「[*アプリを組織のアプリ カタログに公開する*](/microsoftteams/tenant-apps-catalog-teams)」の記事を参照してください。 この機能は、Microsoft Office 365 テナントの管理者特権を持つ Teams ユーザーのみが管理できます。

### <a name="publish-to-appsource"></a>AppSource への公開

AppSource (旧称 Office ストア) は、Office アドインや SharePoint アドインなど、他の Office 365 の拡張機能だけでなく、Microsoft Teams アプリの配布場所としても有効活用できます。[AppSource にアプリを送信](./appsource/publish.md)するには、ガイドラインに従ってください。

## <a name="government-community-cloud-gcc-organizations"></a>Government Community Cloud (GCC) 組織

### <a name="upload-your-custom-app-directly-to-teams"></a>カスタムアプリを Teams に直接アップロードする

 GCC テナント管理者として、カスタムアプリをテナント環境にアップロードするかどうか、およびテナントのアプリカタログに公開するかどうかを決定します。 Microsoft はカスタムアプリケーションを所有または制御していないため、すべてのエンドポイントが組織の要件に準拠していることを確認する必要があります。 また、アプリソリューションに bot またはメッセージの内線番号が含まれている場合は、次のように [Bot フレームワーク](https://dev.botframework.com/) 登録を完了する必要があります。

1. [ **チャネルへの接続** ] ページの [ **おすすめのチャネルの追加**] で、[ **Teams**] を選択します。
1. [ **MSTeams の構成** ] ページに移動します (以下を*参照* )。
1. [ **メッセージング** ] の下にある [ **Microsoft Teams for Government** ] ラジオボタンをクリックします。
1. ページの左下隅にある [ **保存**] を選択します。  

>[!IMPORTANT]
> Teams の商用構成を使用して、カスタムアプリを GCC 環境にアップロード/サイドロードすることはできません。 GCC 準拠の構成については、「 **Government のお客様向け Microsoft Teams** 」ラジオボタンを選択する必要があります。

![Teams のメッセージ構成ページ](../../assets/images/gcc-configure.png)

> [!NOTE]
>
> * 前述の GCC 環境でのアップロード手順は、Teams カスタムアプリに適用されます。 </br>
> * 既定では、準拠している Microsoft アプリが GCC 環境で有効になっています (Teams)。
> * サードパーティ製アプリはテナントレベルで無効になっており、組織のアプリの [アクセス許可ポリシー](/microsoftteams/teams-app-permission-policies)によって管理する必要があります。 すべてのサードパーティ製アプリを確認して、組織のポリシーと手順に沿っていることを確認してください。

> [!TIP]
>
> Microsoft 365 開発者パートナーは、 [microsoft 365 アプリ証明書プログラム](/microsoft-365-app-certification/overview)を使用して、サードパーティの Teams アプリのセキュリティ、データ処理、コンプライアンスの詳細を提供します。 「 [Microsoft Teams App サーティフィケーション](/microsoftteams/platform/concepts/deploy-and-publish/appsource/post-publish/application-certification) *」も参照してください*。
</br></br>
