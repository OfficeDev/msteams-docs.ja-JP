---
title: 会議の通話と会議ボットを登録Microsoft Teams
description: 新しい音声/ビデオ通話ボットを登録する方法についてMicrosoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: ボットのオーディオ/ビデオ オーディオ ビデオ メディアを呼び出す
ms.openlocfilehash: 5013ebcbce0bc94199e846f20fc6ee52238d302f1dd1b05872245ef2c6e32d91
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57709571"
---
# <a name="register-calls-and-meetings-bot-for-microsoft-teams"></a>会議の通話と会議ボットを登録Microsoft Teams

音声またはビデオ通話とオンライン会議に参加するボットは、ボットの登録にMicrosoft Teams追加機能を備える通常のボットです。

* 新しいバージョンのアプリ マニフェストTeams設定が 2 つ追加 `supportsCalling` されています `supportsVideo` 。 これらの設定は、アプリ マニフェスト[の](../../resources/dev-preview/developer-preview-intro.md)開発者プレビュー バージョンTeams含まれています。
* [Microsoft Graphアクセス許可は](./registering-calling-bot.md#add-graph-permissions)、ボットの Microsoft App ID 用に構成する必要があります。
* 電話Graphオンライン会議 API のアクセス許可には、テナント管理者の同意が必要です。

## <a name="new-manifest-settings"></a>新しいマニフェスト設定

通話とオンライン会議ボットには、manifest.jsでボットの音声またはビデオを有効にする次の 2 つの追加設定Teams。

* `bots[0].supportsCalling`. 存在し、に設定 `true` されている場合、Teamsボットが通話やオンライン会議に参加できます。
* `bots[0].supportsVideo`. 存在してに設定されている `true` 場合は、Teamsがビデオをサポートしているという情報が表示されます。

これらの値の呼び出しと会議ボットmanifest.jsスキーマの検証を IDE で適切に行う場合は、次のように属性を `$schema` 変更できます。

```json
"$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
```

次のセクションでは、新しいボットを作成したり、既存のボットに通話機能を追加することができます。

## <a name="create-new-bot-or-add-calling-capabilities"></a>新しいボットを作成するか、通話機能を追加する

ボットの作成の詳細については、「ボット[を作成する」を参照Teams。](../how-to/create-a-bot-for-teams.md)

**新しいボットを作成するには、Teams**

1. 新しいボットを作成するには、このリンクを使用します `https://dev.botframework.com/bots/new` 。 または、ボット フレームワーク ポータルで [ボットの作成] ボタンを選択した場合は、azure アカウントが必要な Microsoft Azure でボットを作成します。
1. 新しいチャネルTeamsします。
1. [チャネル]**ページの**[呼び出しTeams選択します。 [ **通話を有効にする**] を選択し、受信通知を受信する HTTPS URL を使用して **Webhook (通話用)** を更新します `https://contoso.com/teamsapp/api/calling` 。 詳細については、「チャネルの [構成」を参照してください](/bot-framework/portal-configure-channels)。

    ![チャネルTeams構成する](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

次のセクションでは、通話およびオンライン会議でサポートされているアプリケーションのアクセス許可の一覧を示します。

## <a name="add-graph-permissions"></a>アクセス許可Graph追加する

このGraphは、アプリがリソースに対して持つアクセスを制御するための詳細なアクセス許可を提供します。 アプリ要求に対するアクセス許可Graph決定します。 呼びGraph API は、サインインしているユーザーが存在せずに実行されるアプリで使用されるアプリケーションのアクセス許可をサポートします。 テナント管理者は、アプリケーションのアクセス許可に同意する必要があります。

### <a name="application-permissions-for-calls"></a>呼び出しのアプリケーションのアクセス許可

次の表に、呼び出しに対するアプリケーションのアクセス許可の一覧を示します。

|アクセス許可    |表示文字列   |説明 |管理者の同意が必要 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| Calls.Initiate.All |アプリ プレビューから発信 1:1 通話を開始します。 |アプリで、サインインしているユーザーがいなくても、1 人のユーザーに発信し、組織のディレクトリ内のユーザーに通話を転送することができるようにします。|はい|
| Calls.InitiateGroupCall.All |アプリ プレビューからグループの発信呼び出しを開始します。 |アプリで、サインインしているユーザーがいなくても、複数のユーザーに発信し、組織内の会議に参加者を追加することができるようにします。|はい|
| Calls.JoinGroupCall.All |アプリ のプレビューとしてグループ通話と会議に参加します。 |アプリで、サインインしているユーザーがいなくても、組織のグループ通話やスケジュールされた会議に参加することができるようにします。 アプリは、テナント内の会議にディレクトリ ユーザーの特権で参加します。|はい|
| Calls.JoinGroupCallasGuest.All |グループ通話と会議にゲスト プレビューとして参加します。 |アプリで、サインインしているユーザーがいなくても、組織のグループ通話とスケジュールされた会議に匿名で参加することができるようにします。 アプリは、テナント内の会議にゲストとして参加します。|はい|
| Calls.AccessMedia.All |アプリ プレビューとして通話のメディア ストリームにアクセスします。 |アプリで、サインインしているユーザーがいなくても、通話内のメディア ストリームに直接アクセスすることができるようにします。|はい|

> [!IMPORTANT]
> メディア アクセス API を使用して、アプリケーションがアクセスしたり、そのメディア コンテンツ レコードまたは記録からデータを派生したりした通話や会議からメディア コンテンツを記録したり、保持したりすることはできません。 最初に API[ `updateRecordingStatus` を呼び](/graph/api/call-updaterecordingstatus)出して、記録が開始されたと示し、その API から成功の返信を受け取る必要があります。 アプリケーションが会議または通話の録音を開始する場合は、API を呼び出す前に録音を終了して、録音が終了した `updateRecordingStatus` かどうかを示す必要があります。

### <a name="application-permissions-for-online-meetings"></a>オンライン会議のアプリケーションのアクセス許可

次の表に、オンライン会議のアプリケーションアクセス許可の一覧を示します。

|アクセス許可    |表示文字列   |説明 |管理者の同意が必要 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| OnlineMeetings.Read.All |アプリ プレビューからオンライン会議の詳細を読み取る|サインインしているユーザーなしで、アプリが組織内のオンライン会議の詳細を読み取るを許可します。|はい|
| OnlineMeetings.ReadWrite.All |ユーザーに代わってアプリ プレビューからオンライン会議を読み取り、作成する|サインインしているユーザーなしで、アプリがユーザーに代わって組織内でオンライン会議を作成できます。|必要|

### <a name="assign-permissions"></a>アクセス許可の割り当て

Azure portal を使用して、ボットのアプリケーションのアクセス許可を[](https://aka.ms/aadapplist)事前に構成する必要があります[(AAD) V1](/azure/active-directory/develop/azure-ad-endpoint-comparison)エンドポイントを使用する場合は、Azure Active Directoryを使用します。

### <a name="get-tenant-administrator-consent"></a>テナント管理者の同意を取得する

AAD V1 エンドポイントを使用するアプリの場合、テナント管理者は、アプリが組織にインストールされている [ときに Azure portal](https://portal.azure.com) を使用してアプリケーションのアクセス許可に同意できます。 または、構成したアクセス許可に管理者が同意できるサインアップ エクスペリエンスをアプリに提供することもできます。 管理者の同意が AAD によって記録された後、アプリは再び同意を要求することなくトークンを要求できます。

管理者に頼って、Azure portal でアプリに必要なアクセス許可を [付与できます](https://portal.azure.com)。 AAD V2 エンドポイントを使用して管理者にサインアップ エクスペリエンスを提供する方が良い `/adminconsent` 方法です。 詳細については、「管理者の [同意 URL の作成に関する手順」を参照してください](https://developer.microsoft.com/graph/docs/concepts/auth_v2_service#3-get-administrator-consent)。

> [!NOTE]
> テナント管理者の同意 URL を作成するには、アプリ登録ポータルで構成されたリダイレクト URI または返信 URL [が](https://apps.dev.microsoft.com/) 必要です。 ボットの返信 URL を追加するには、ボット登録にアクセスし、[高度なオプション] [**アプリケーション** マニフェストの編集  >  **] を選択します**。 リダイレクト URL をコレクションに追加 `replyUrls` します。

> [!IMPORTANT]
> アプリケーションのアクセス許可を変更する場合は、管理者の同意プロセスも繰り返す必要があります。 アプリ登録ポータルで行われた変更は、テナントの管理者が同意を再適用するまで反映されません。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [着信通知](~/bots/calls-and-meetings/call-notifications.md)
