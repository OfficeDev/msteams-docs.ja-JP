---
title: Microsoft Teams の通話と会議ボットを登録する
description: このモジュールでは、新しいオーディオ/ビデオ通話ボットをMicrosoft Teamsに登録する方法、新しいボットを作成する方法、通話機能を追加する方法、グラフのアクセス許可を追加する方法について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 74e786850f11a77cea5cc0980febb56d550ae671
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143796"
---
# <a name="register-calls-and-meetings-bot-for-microsoft-teams"></a>Microsoft Teams の通話と会議ボットを登録する

音声またはビデオ通話やオンライン会議に参加するボットは、ボットの登録に使用される次の追加機能を備えた通常のMicrosoft Teams ボットです。

* Teams アプリ マニフェストの新しいバージョンには、`supportsCalling` と `supportsVideo` の 2 つの追加設定があります。 これらの設定は、 [Microsoft Teams のマニフェスト スキーマ](../../resources/schema/manifest-schema.md)に含まれています。
* [Microsoft Graph アクセス許可](./registering-calling-bot.md#add-graph-permissions)は、ボットの Microsoft アプリ ID に対して構成する必要があります。
* Graph 通話とオンライン会議 API のアクセス許可には、テナント管理者の同意が必要です。

## <a name="new-manifest-settings"></a>新しいマニフェスト設定

通話とオンライン会議ボットには、 Teams でボットのオーディオまたはビデオを有効にする manifest.json に次の 2 つの追加設定があります。

* `bots[0].supportsCalling`。この設定が存在し、かつ `true` に設定されている場合、Teams はボットが通話やオンライン会議に参加することを許可します。
* `bots[0].supportsVideo`。この設定が存在し、かつ `true` に設定されている場合は、ボットがビデオをサポートしていることを Teams が認識します。

IDE でこれらの値について、通話と会議ボットの manifest.json スキーマを適切に検証する場合は、次のように `$schema` 属性を変更できます。

```json
"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
```

次のセクションでは、新しいボットを作成したり、既存のボットに通話機能を追加したりできます。

## <a name="create-new-bot-or-add-calling-capabilities"></a>新しいボットの作成または通話機能の追加

ボットの作成については、「[Teams 用のボットを作成する](../how-to/create-a-bot-for-teams.md)」を参照してください。

Teams 用の新しいボットを作成するには:

1. このリンク (`https://dev.botframework.com/bots/new`) を使用して新しいボットを作成します。または、Bot Framework ポータルで **[ボットの作成]** ボタンを選択する場合は、Microsoft Azure でボットを作成します。この場合、Azure アカウントを持っている必要があります。
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
| Calls.InitiateGroupCall.All |アプリ プレビューからの発信グループ通話の開始。 |アプリで、サインインしているユーザーがいなくても、複数のユーザーに発信し、組織内の会議に参加者を追加することができるようにします。|はい|
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

Azure AD V1 エンドポイントを使用するアプリの場合、テナント管理者は、組織にアプリがインストールされるときに [Microsoft Azure ポータル](https://portal.azure.com)を使用して、アプリケーションのアクセス許可に同意できます。または、アプリでサインアップ エクスペリエンスを提供して、管理者が構成済みのアクセス許可に同意できるようにすることができます。管理者の同意が Azure AD によって記録されると、アプリは再度同意を要求しなくてもトークンを要求できます。

管理者に依頼して、 [Microsoft Azure ポータル](https://portal.azure.com)でアプリに必要なアクセス許可を付与できます。より優れた選択肢は Azure AD v2 `/adminconsent` エンドポイントを使用して管理者にサインアップ エクスペリエンスを提供することです。詳細については、「[管理者同意 URL の作成手順](/graph/auth-v2-service#3-get-administrator-consent)」を参照してください。

> [!NOTE]
> テナント管理者の同意 URL を作成するには、 [アプリ登録ポータル](https://apps.dev.microsoft.com/) で構成されたリダイレクト URI または応答 URL が必要です。 ボットの応答 URL を追加するには、ボットの登録にアクセスし、[**詳細オプション** > **アプリケーション マニフェストの編集**] を選択します。 リダイレクト URL をコレクション `replyUrls` に追加します。

> [!IMPORTANT]
> アプリケーションのアクセス許可に変更を加える場合は常に、管理者の同意プロセスも繰り返す必要があります。 アプリ登録ポータルで行われた変更は、テナント管理者が同意を再適用するまで反映されません。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **Graph** |
|---------------|----------|--------|
| 通話ボットと会議ボット | サンプル アプリでは、ボットが通話を作成し、会議に参加し、通話を転送する方法を示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-calling-meeting/csharp) |

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

[ステップ バイ ステップ ガイド](../../sbs-calling-and-meeting.yml)に従って、ボットで通話と会議を設定します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [着信通知](~/bots/calls-and-meetings/call-notifications.md)

## <a name="see-also"></a>関連項目

* [着信通知](~/bots/calls-and-meetings/call-notifications.md)
* [ローカル PC で通話ボットとオンライン会議ボットを開発する](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
* [アプリのアクセス許可を表示し、管理者の同意を与える](/MicrosoftTeams/app-permissions-admin-center)
