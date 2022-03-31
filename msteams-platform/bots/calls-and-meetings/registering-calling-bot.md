---
title: Microsoft Teams の通話と会議ボットを登録する
description: 新しい音声/ビデオ通話ボットの登録、Microsoft Teamsボットの作成、通話機能の追加、グラフのアクセス許可の追加を行う方法について学習します。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: ボットのオーディオ/ビデオ オーディオ ビデオ メディアを呼び出す
ms.openlocfilehash: 1a90e430ba0c5bc4ae1ab246baa85a5d33507a43
ms.sourcegitcommit: 52af681132e496a57b18f468c5b73265a49a5f44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2022
ms.locfileid: "64590767"
---
# <a name="register-calls-and-meetings-bot-for-microsoft-teams"></a>Microsoft Teams の通話と会議ボットを登録する

音声またはビデオ通話とオンライン会議に参加するボットは、ボットの登録にMicrosoft Teams追加機能を備える通常のボットです。

* 新しいバージョンのアプリ マニフェストTeams設定が 2 つ追加されています `supportsCalling` `supportsVideo`。 これらの設定は、マニフェスト スキーマ[のマニフェスト スキーマに含Microsoft Teams](../../resources/schema/manifest-schema.md)。
* [Microsoft Graphアクセス許可は](./registering-calling-bot.md#add-graph-permissions)、ボットの Microsoft App ID 用に構成する必要があります。
* 電話Graphオンライン会議 API のアクセス許可には、テナント管理者の同意が必要です。

## <a name="new-manifest-settings"></a>新しいマニフェスト設定

呼び出しとオンライン会議ボットには、マニフェスト.json に次の 2 つの追加設定が含まれています。この設定を使用すると、ボットのオーディオまたはビデオが有効Teams。

* `bots[0].supportsCalling`. 存在し、に設定されている`true`場合、Teams、ボットが通話やオンライン会議に参加できます。
* `bots[0].supportsVideo`. 存在し、に設定されている`true`場合は、Teamsがビデオをサポートしているという情報が表示されます。

これらの値の呼び出しと会議ボットの manifest.json `$schema` スキーマを IDE で適切に検証する場合は、次のように属性を変更できます。

```json
"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
```

次のセクションでは、新しいボットを作成したり、既存のボットに通話機能を追加することができます。

## <a name="create-new-bot-or-add-calling-capabilities"></a>新しいボットを作成するか、通話機能を追加する

ボットの作成の詳細については、「ボット[を作成する」](../how-to/create-a-bot-for-teams.md)を参照Teams。

新しいボットを作成するには、次Teams。

1. 新しいボットを作成するには、このリンクを使用します `https://dev.botframework.com/bots/new`。 または、ボット フレームワーク ポータルで [ボットの作成] ボタンを選択した場合は、azure アカウントが必要な Microsoft Azure でボットを作成します。
1. チャネルを追加Teamsします。
1. [チャネル] **ページの** [通話] Teamsを選択します。 [通話 **を有効にする**] を選択し、受信通知を受信する HTTPS URL を使用して **Webhook (通話用)** を更新します `https://contoso.com/teamsapp/api/calling`。 詳細については、「チャネルの [構成」を参照してください](/bot-framework/portal-configure-channels)。

    ![チャネルTeams構成する](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

次のセクションでは、通話およびオンライン会議でサポートされているアプリケーションのアクセス許可の一覧を示します。

## <a name="add-graph-permissions"></a>アクセス許可Graph追加する

このGraphは、アプリがリソースに対して持つアクセスを制御するための詳細なアクセス許可を提供します。 アプリ要求に対するアクセス許可Graph決定します。 呼びGraph API の呼び出し元は、サインインしているユーザーが存在せずに実行されるアプリで使用されるアプリケーションのアクセス許可をサポートします。 テナント管理者は、アプリケーションのアクセス許可に同意する必要があります。

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
> メディア アクセス API を使用して、アプリケーションがアクセスしたり、そのメディア コンテンツ レコードまたは記録からデータを派生したりした通話や会議からメディア コンテンツを記録したり、保持したりすることはできません。 最初に API [を呼び出`updateRecordingStatus`](/graph/api/call-updaterecordingstatus)して、記録が開始されたと示し、その API から成功の返信を受け取る必要があります。 アプリケーションが会議または通話の `updateRecordingStatus` 録音を開始する場合は、API を呼び出す前に録音を終了して、録音が終了したかどうかを示す必要があります。

### <a name="application-permissions-for-online-meetings"></a>オンライン会議のアプリケーションのアクセス許可

次の表に、オンライン会議のアプリケーションアクセス許可の一覧を示します。

|アクセス許可    |表示文字列   |説明 |管理者の同意が必要 |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| OnlineMeetings.Read.All |アプリ プレビューからオンライン会議の詳細を読み取る|サインインしているユーザーなしで、アプリが組織内のオンライン会議の詳細を読み取るを許可します。|はい|
| OnlineMeetings.ReadWrite.All |ユーザーに代わってアプリ プレビューからオンライン会議を読み取り、作成する|サインインしているユーザーなしで、アプリがユーザーに代わって組織内でオンライン会議を作成できます。|はい|

### <a name="assign-permissions"></a>アクセス許可の割り当て

Microsoft Azure Active Directory (Azure AD) V1 エンドポイントを使用する場合は、[Microsoft Azure](https://aka.ms/aadapplist) ポータルを使用して、ボットのアプリケーションアクセス許可を事前[に構成する必要があります](/azure/active-directory/develop/azure-ad-endpoint-comparison)。

### <a name="get-tenant-administrator-consent"></a>テナント管理者の同意を取得する

Azure AD V1 エンドポイントを使用するアプリの場合、テナント管理者は、アプリが組織にインストール[されている場合、Microsoft Azure](https://portal.azure.com) ポータルを使用してアプリケーションのアクセス許可に同意できます。 または、構成したアクセス許可に管理者が同意できるサインアップ エクスペリエンスをアプリに提供することもできます。 管理者の同意がユーザーによって記録Azure AD、アプリは再び同意を要求することなくトークンを要求できます。

管理者に頼って、アプリが必要とするアクセス許可を管理者ポータルMicrosoft Azure[できます](https://portal.azure.com)。 より良い方法は、管理者が V2 エンドポイントを使用してサインアップ エクスペリエンスAzure ADです`/adminconsent`。 詳細については、「管理者の [同意 URL を作成する手順」を参照してください](/graph/auth-v2-service#3-get-administrator-consent)。

> [!NOTE]
> テナント管理者の同意 URL を作成するには、アプリ登録ポータルで構成されたリダイレクト URI または返信 URL [が](https://apps.dev.microsoft.com/) 必要です。 ボットの返信 URL を追加するには、ボット登録にアクセスし、[**Advanced OptionsEdit** >  アプリケーション マニフェスト] **を選択します**。 リダイレクト URL をコレクションに追加 `replyUrls` します。

> [!IMPORTANT]
> アプリケーションのアクセス許可を変更する場合は、管理者の同意プロセスも繰り返す必要があります。 アプリ登録ポータルで行われた変更は、テナントの管理者が同意を再適用するまで反映されません。

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **Graph** |
|---------------|----------|--------|
| 通話と会議ボット | このサンプル アプリでは、ボットが通話の作成、会議への参加、通話の転送を行う方法を説明します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-calling-meeting/csharp) |

## <a name="step-by-step-guide"></a>ステップ バイ ステップのガイド

ボットで [通話と会議を](../../sbs-calling-and-meeting.yml) 設定するには、手順に従ってガイドを実行します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [着信通知](~/bots/calls-and-meetings/call-notifications.md)

## <a name="see-also"></a>関連項目

* [着信通知](~/bots/calls-and-meetings/call-notifications.md)
* [ローカル PC で通話およびオンライン会議ボットを開発する](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
* [アプリのアクセス許可を表示し、管理者の同意を付与する](/MicrosoftTeams/app-permissions-admin-center)
