---
title: Microsoft Teams での通話と会議のボットの登録
description: Microsoft Teams 用の新しい音声ビデオを呼び出すボットを登録する方法について説明します。
keywords: ボット音声/ビデオ音声ビデオメディアの呼び出し
ms.openlocfilehash: 9a246c9b1a5aae230881b468afef6c205d5bdecf
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801205"
---
# <a name="registering-a-calling-bot-for-microsoft-teams"></a>Microsoft Teams 用の呼び出しボットの登録

音声ビデオ通話やオンライン会議に参加する bot は、次のようないくつかの機能を備えた通常の Microsoft Teams bot です。

* Teams アプリマニフェストの新バージョンとして、2つの追加設定とが用意さ `supportsCalling` `supportsVideo` れています。 これらの設定は、Microsoft Teams アプリマニフェストの[開発者プレビュー](../../resources/dev-preview/developer-preview-intro.md)バージョンに含まれています。
* [Microsoft Graph のアクセス許可](./registering-calling-bot.md#add-microsoft-graph-permissions)は、ボットの MICROSOFT アプリ ID に対して構成する必要があります。
* Microsoft Graph の呼び出しとオンライン会議の Api のアクセス許可には、テナント管理者の同意が必要です。

詳細について説明します。

## <a name="new-manifest-settings"></a>新しいマニフェスト設定

通話とオンライン会議のボットには、Teams のボットに対して音声/ビデオを有効にするための manifest.jsに、次の2つの追加設定があります。

* `bots[0].supportsCalling`. が存在し、に設定されている場合 `true` 、チームは、お客様が bot に通話とオンライン会議への参加を許可します。
* `bots[0].supportsVideo`. が存在し、に設定されている場合 `true` 、Teams は、ボットがビデオをサポートしていることを認識します。

このような値について、IDE で、呼び出し側と会議のスキーマの manifest.jsを適切に検証するには、次のように属性を変更し `$schema` ます。

```json
"$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
```

## <a name="creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot"></a>新しい bot を作成するか、既存の bot に呼び出し機能を追加する

新しい bot を作成する方法については、「 [Microsoft Teams の bot を作成する](../how-to/create-a-bot-for-teams.md)」トピックで詳しく説明されていますが、ここではその一部を繰り返します。

1. 新しい bot を作成するには、このリンクを使用します。 `https://dev.botframework.com/bots/new` 代わりに、Bot フレームワークポータルで [ *bot を作成*する] ボタンを選択すると、Microsoft azure に bot が作成され、azure アカウントが必要になります。
1. Microsoft Teams チャネルを追加します。 Microsoft Teams channel ページの [通話中] タブをクリックし、[**通話を有効にする**] を選択してから、受信通知を受け取る HTTPS URL で**Webhook (通話用)** を更新します。たとえば、次のように `https://contoso.com/teamsapp/api/calling` します。 チャネルを構成する方法の詳細については、「[チャネルの構成](/bot-framework/portal-configure-channels)」を参照してください。
  ![Microsoft Teams のチャネル情報を構成する](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

## <a name="add-microsoft-graph-permissions"></a>Microsoft Graph のアクセス許可を追加する

Microsoft Graph では、アプリがリソースに対して持つアクセス権を制御する詳細なアクセス許可を公開しています。 開発者は、アプリが要求する Microsoft Graph のアクセス許可を決定します。  Microsoft Graph の呼び出し元の Api は、サインインしているユーザーなしで実行されるアプリで使用される_アプリケーションのアクセス許可_をサポートします。  テナント管理者は、アプリケーションのアクセス許可に同意を付与する必要があります。 これらのアクセス許可の一覧を以下に示します。

### <a name="application-permissions-calls"></a>アプリケーションのアクセス許可: 呼び出し

|アクセス許可    |表示文字列   |説明 |管理者の同意が必要 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
|_Calls.Initiate.All_|アプリからの発信 1 対 1 通話の開始 (プレビュー)|アプリで、サインインしているユーザーがいなくても、1 人のユーザーに発信し、組織のディレクトリ内のユーザーに通話を転送することができるようにします。|はい|
|_Calls.InitiateGroupCall.All_|アプリからの発信グループ通話の開始 (プレビュー)|アプリで、サインインしているユーザーがいなくても、複数のユーザーに発信し、組織内の会議に参加者を追加することができるようにします。|はい|
|_Calls.JoinGroupCall.All_|グループ通話と会議にアプリとして参加する (プレビュー)|アプリで、サインインしているユーザーがいなくても、組織のグループ通話やスケジュールされた会議に参加することができるようにします。 このアプリは、ディレクトリ ユーザーの特権を使用してテナントの会議に参加します。|はい|
|_Calls.JoinGroupCallasGuest.All_|グループ通話と会議にゲストとして参加する (プレビュー)|アプリで、サインインしているユーザーがいなくても、組織のグループ通話とスケジュールされた会議に匿名で参加することができるようにします。 このアプリは、テナントの会議にゲストとして参加します。|はい|
|_通話メディアを呼び出します。_ <sup>_以下を参照_</sup>|通話内のメディア ストリームにアプリとしてアクセスする (プレビュー)|アプリで、サインインしているユーザーがいなくても、通話内のメディア ストリームに直接アクセスすることができるようにします。|はい|

> [!IMPORTANT]
> Microsoft Graph API を使用して、ボットがアクセスする通話または会議からメディアコンテンツを録音または保存する**ことはできません**。

### <a name="application-permissions-online-meetings"></a>アプリケーションのアクセス許可: オンライン会議

|アクセス許可    |表示文字列   |説明 |管理者の同意が必要 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
|_OnlineMeetings.Read.All_|アプリからオンライン会議の詳細を読み取る (プレビュー)|アプリで、サインインしているユーザーがいなくても、組織内のすべてのオンライン会議を読み取ることができるようにします。|はい|
|_OnlineMeetings.ReadWrite.All_|サインインしているユーザーの代わりにアプリが行うオンライン会議の読み取りと作成 (プレビュー)|アプリで、サインインしているユーザーがいなくても、ユーザーの代わりに、組織内のオンライン会議を作成することができるようにします。|はい|

### <a name="assigning-permissions"></a>権限を割り当てる

前もって bot のアプリケーションアクセス許可を構成する必要があります。 [ここで](/graph/docs/concepts/auth_register_app_v2)説明するように、 [Microsoft アプリ登録ポータル](https://apps.dev.microsoft.com/)を使用することをお勧めします。これは、ボットが構成されている場所です。ただし、 [AZURE AD V1 エンドポイント](/azure/active-directory/develop/azure-ad-endpoint-comparison)を使用したい場合は、 [azure ポータル](https://aka.ms/aadapplist)を使用することもできます。

### <a name="getting-tenant-administrator-consent"></a>テナント管理者の同意を取得する

Azure AD V1 エンドポイントを使用するアプリの場合、テナント管理者は、アプリが組織にインストールされているときに、 [azure portal](https://portal.azure.com)を使用してアプリケーションのアクセス許可に同意することができます。または、構成したアクセス許可を管理者が承認できるようにするためのサインアップの機能をアプリで提供することができます。 管理者の同意が Azure AD によって記録されると、アプリは同意を要求せずにトークンを要求できます。

[Azure ポータル](https://portal.azure.com)でアプリに必要なアクセス許可を管理者に付与することができます。ただし、多くの場合、Azure AD V2 エンドポイントを使用して管理者にサインアップのための機能を提供することをお勧め `/adminconsent` します。  詳細については、「[管理者の同意の URL](https://developer.microsoft.com/graph/docs/concepts/auth_v2_service#3-get-administrator-consent)を作成する」の手順を参照してください。

> [!NOTE]
> テナント管理者の同意 URL を作成するには、[アプリ登録ポータル](https://apps.dev.microsoft.com/)に構成されたリダイレクト URI/応答 url が必要です。 Bot の応答 Url を追加するには、ボット登録にアクセスし、[Advanced Options-> 編集アプリケーションマニフェスト] を選択します。  リダイレクト URL をコレクションに追加 `replyUrls` します。

> [!IMPORTANT]
> アプリケーションのアクセス許可を変更するときは常に、管理者の同意プロセスも繰り返す必要があります。 アプリ登録ポータルで行われた変更は、テナント管理者が同意を再適用するまで反映されません。
