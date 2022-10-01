---
title: Microsoft Teams の通話と会議ボットを登録する
description: Microsoft Teams 用の新しいオーディオ/ビデオ通話ボットを登録する方法、新しいボットを作成する方法、通話機能を追加する方法、グラフのアクセス許可を追加する方法について説明します。 通話の作成、会議への参加、通話の転送を行うサンプル。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 3fe8d0adde45242738b8023c5478c24769561d1c
ms.sourcegitcommit: 53818e55dfe0dbdf874d578a40982f7db444f89b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2022
ms.locfileid: "68319938"
---
# <a name="register-calls-and-meetings-bot-for-microsoft-teams"></a>Microsoft Teams の通話と会議ボットを登録する

音声またはビデオ通話やオンライン会議に参加するボットは、ボットの登録に使用される次の追加機能を備えた通常のMicrosoft Teams ボットです。

* Teams アプリ マニフェストの新しいバージョンには、`supportsCalling` と `supportsVideo` の 2 つの追加設定があります。 これらの設定は、 [Microsoft Teams のマニフェスト スキーマ](../../resources/schema/manifest-schema.md)に含まれています。
* [Microsoft Graph アクセス許可](./registering-calling-bot.md#add-graph-permissions)は、ボットの Microsoft アプリ ID に対して構成する必要があります。
* Graph 通話とオンライン会議 API のアクセス許可には、テナント管理者の同意が必要です。

## <a name="new-manifest-settings"></a>新しいマニフェスト設定

通話とオンライン会議ボットには、 Teams でボットのオーディオまたはビデオを有効にする manifest.json に次の 2 つの追加設定があります。

* `bots[0].supportsCalling`. If present and set to `true`, Teams allows your bot to participate in calls and online meetings.
* `bots[0].supportsVideo`. If present and set to `true`, Teams knows that your bot supports video.

IDE でこれらの値について、通話と会議ボットの manifest.json スキーマを適切に検証する場合は、次のように `$schema` 属性を変更できます。

```json
"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
```

次のセクションでは、新しいボットを作成したり、既存のボットに通話機能を追加したりできます。

## <a name="create-new-bot-or-add-calling-capabilities"></a>新しいボットの作成または通話機能の追加

ボットの作成については、「[Teams 用のボットを作成する](../how-to/create-a-bot-for-teams.md)」を参照してください。

Teams 用の新しいボットを作成するには:

1. Use this link to create a new bot, `https://dev.botframework.com/bots/new`. Alternately, if you select the **Create a bot** button in the Bot Framework portal, you create your bot in Microsoft Azure, for which you must have an Azure account.
1. Teams チャネルを追加します。
1. チャネル ページの **[ 通話 ]** タブを選択します。 **[ 通話を有効にする ]** を選択し、たとえば `https://contoso.com/teamsapp/api/calling` のような、着信通知を受信する HTTPS URL を使用して **Webhook (通話用)** を更新します。 詳細については、 「[チャネルの構成](/bot-framework/portal-configure-channels)」を参照してください。

    ![Teams チャネル情報を構成する](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

次のセクションでは、通話とオンライン会議でサポートされているアプリケーションのアクセス許可の一覧を示します。

## <a name="add-graph-permissions"></a>Graph にアクセス許可を追加する

Graph は、アプリがリソースに対して持つアクセスを制御するためのきめ細かなアクセス許可を提供します。 アプリが要求する Graph に対するアクセス許可を決定します。 API を呼び出す Graph は、サインインしているユーザーがいない状態で実行されるアプリによって使用されるアプリケーションのアクセス許可をサポートします。 テナント管理者は、アプリケーションのアクセス許可に同意する必要があります。

### <a name="application-permissions-for-calls"></a>通話に対するアプリケーションのアクセス許可

次の表に、通話に対するアプリケーションのアクセス許可の一覧を示します。

|アクセス許可    |表示文字列   |説明 |管理者の同意が必要 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| Calls.Initiate.All |アプリ プレビューからの 1 対 1 通話の発信開始。 |アプリで、サインインしているユーザーがいなくても、1 人のユーザーに発信し、組織のディレクトリ内のユーザーに通話を転送することができるようにします。|はい|
| Calls.InitiateGroupCall.All |発信 1:1 を開始し、アプリ プレビューから通話をグループ化します。 |アプリが 1 人のユーザー、複数のユーザーに発信通話を発信し、通話を転送し、サインインしているユーザーなしで組織内の会議に参加者を追加できるようにします。|はい|
| Calls.JoinGroupCall.All |グループ通話と会議にアプリ プレビューとして参加する。 |アプリで、サインインしているユーザーがいなくても、組織のグループ通話やスケジュールされた会議に参加することができるようにします。 このアプリは、ディレクトリ ユーザーの特権を使用してテナントの会議に参加します。|はい|
| Calls.JoinGroupCallasGuest.All |グループ通話と会議にゲスト プレビューとして参加する。 |アプリで、サインインしているユーザーがいなくても、組織のグループ通話とスケジュールされた会議に匿名で参加することができるようにします。 このアプリは、テナントの会議にゲストとして参加します。|はい|
| Calls.AccessMedia.All |通話内のメディア ストリームにアプリ プレビューとしてアクセスする。 |アプリで、サインインしているユーザーがいなくても、通話内のメディア ストリームに直接アクセスすることができるようにします。|はい|

> [!IMPORTANT]
> Media Access API を使用して、アプリケーションがアクセスする通話や会議からのメディア コンテンツを記録したり、そのメディア コンテンツの記録やその他の記録からデータを取得したりすることはできません。 最初に [`updateRecordingStatus` API](/graph/api/call-updaterecordingstatus) を呼び出して、記録が開始されたことを示し、その API から成功の応答を受け取る必要があります。 アプリケーションが会議または通話の記録を開始する場合は、 `updateRecordingStatus` API を呼び出して記録が終了したことを示す前に記録を終了する必要があります。

### <a name="application-permissions-for-online-meetings"></a>オンライン会議のアプリケーションのアクセス許可

次の表に、オンライン会議のアプリケーションのアクセス許可の一覧を示します。

|アクセス許可    |表示文字列   |説明 |管理者の同意が必要 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| OnlineMeetings.Read.All |アプリ プレビューからオンライン会議の詳細を読み取る|アプリで、サインインしているユーザーがいなくても、組織内のオンライン会議の詳細を読み取ることができるようにします。|はい|
| OnlineMeetings.ReadWrite.All |ユーザーの代わりにアプリ プレビューが行うオンライン会議の読み取りと作成 |アプリで、サインインしているユーザーがいなくても、ユーザーの代わりに、組織内のオンライン会議を作成することができるようにします。|はい|

### <a name="assign-permissions"></a>アクセス許可の割り当て

[Microsoft Azure Active Directory (Azure AD) V1 エンドポイント](/azure/active-directory/develop/azure-ad-endpoint-comparison)を使用する場合は、 [Microsoft Azure ポータル](https://portal.azure.com)を使用して、ボットのアプリケーションのアクセス許可を事前に構成する必要があります。

### <a name="get-tenant-administrator-consent"></a>テナント管理者の同意を取得する

For apps using the Azure AD V1 endpoint, a tenant administrator can consent to the application permissions using the [Microsoft Azure portal](https://portal.azure.com) when your app is installed in their organization. Alternately, you can provide a sign-up experience in your app through which administrators can consent to the permissions you configured. Once administrator consent is recorded by Azure AD, your app can request tokens without having to request consent again.

You can rely on an administrator to grant the permissions your app needs at the [Microsoft Azure portal](https://portal.azure.com). A better option is to provide a sign-up experience for administrators by using the Azure AD V2 `/adminconsent` endpoint. For more information, see [instructions on constructing an Admin consent URL](/graph/auth-v2-service#3-get-administrator-consent).

> [!NOTE]
> テナント管理者の同意 URL を作成するには、 [アプリ登録ポータル](https://apps.dev.microsoft.com/) で構成されたリダイレクト URI または応答 URL が必要です。 ボットの応答 URL を追加するには、ボットの登録にアクセスし、[**詳細オプション** > **アプリケーション マニフェストの編集**] を選択します。 リダイレクト URL をコレクション `replyUrls` に追加します。

> [!IMPORTANT]
> アプリケーションのアクセス許可に変更を加える場合は常に、管理者の同意プロセスも繰り返す必要があります。 アプリ登録ポータルで行われた変更は、テナント管理者が同意を再適用するまで反映されません。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **C#** |
|---------------|----------|--------|
| 通話ボットと会議ボット | サンプル アプリでは、ボットが通話を作成し、会議に参加し、通話を転送する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-calling-meeting/csharp) |
| リアルタイム会議イベント |サンプル アプリでは、ボットがリアルタイムの会議イベントを受信する方法を示します。|[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

[ステップ バイ ステップ ガイド](../../sbs-calling-and-meeting.yml)に従って、ボットで通話と会議を設定します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [着信通知](~/bots/calls-and-meetings/call-notifications.md)

## <a name="see-also"></a>関連項目

* [着信通知](~/bots/calls-and-meetings/call-notifications.md)
* [ローカル PC で通話ボットとオンライン会議ボットを開発する](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
* [アプリのアクセス許可を表示し、管理者の同意を与える](/MicrosoftTeams/app-permissions-admin-center)
* [Microsoft Graph でクラウド コミュニケーション API を操作する](/graph/api/resources/communications-api-overview)
