---
title: 会議のトランスクリプトをフェッチするための会議 ID と開催者 ID を取得する
description: 会議のトランスクリプトをフェッチするための会議 ID と開催者 ID の取得のプロセスについて説明します。
ms.localizationpriority: high
ms.topic: concept
ms.openlocfilehash: 9581d65c418032aff2287b4ee0de1ee762a8ffb7
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232393"
---
# <a name="obtain-meeting-id-and-organizer-id"></a>会議 ID と開催者 ID を取得する

アプリは、会議 ID と、会議の開催者のユーザー ID (開催者 ID とも呼ばれます) を使用して、会議のトランスクリプトをフェッチできます。 Graph REST API は、API でパラメーターとして渡される会議 ID と開催者 ID に基づいてトランスクリプトをフェッチします。

> [!NOTE]
> スケジュールされた会議の会議 ID は、未使用の場合、数日で期限切れになることがあります。 会議 URL を使用して会議に参加することで復活できます。 さまざまな種類の会議の有効期限のタイムラインの詳細については、「[会議の有効期限](/microsoftteams/limits-specifications-teams#meeting-expiration)」を参照してください。

トランスクリプトをフェッチするための会議 ID と開催者 ID を取得するには、次の 2 つの方法のいずれかを選択します。

- [変更通知を受信する](#subscribe-to-change-notifications)
- [ボット フレームワークを使用する](#use-bot-framework-to-get-meeting-id-and-organizer-id)

### <a name="subscribe-to-change-notifications"></a>変更通知を受信する

アプリをサブスクライブして、スケジュールされた会議イベントの変更通知を受け取ることができます。 サブスクライブされた会議イベントについてアプリが通知されると、必要な Azure AD アクセス許可によってアプリが承認されていれば、トランスクリプトを取得できます。

アプリは、サブスクライブしている会議イベントの種類に関する通知を受け取ります。

- [ユーザー レベルの通知](#obtain-meeting-details-using-user-level-notification)
- [テナント レベルの通知](#obtain-meeting-details-using-tenant-level-notification)

サブスクライブされた会議イベントがアプリに通知されると、アプリは通知メッセージから会議 ID と開催者 ID を取得できます。 取得した会議の詳細に基づいて、アプリは会議の終了後に会議のトランスクリプトをフェッチできます。

#### <a name="obtain-meeting-details-using-user-level-notification"></a>ユーザー レベルの通知を使用して会議の詳細を取得する

特定のユーザーの会議イベントのトランスクリプトを取得するために、アプリをユーザー レベルの通知にサブスクライブすることを選択します。 そのユーザーの会議がスケジュールされると、アプリに通知されます。 アプリは、カレンダー イベントを使用して会議通知を受け取ることもできます。

アプリをカレンダー イベントにサブスクライブする方法については、「[Microsoft Graph で Outlook リソースの通知を変更する](/graph/outlook-change-notifications-overview)」を参照してください。

次の例を使用して、ユーザー レベルの通知をサブスクライブします。

```http
    
POST https://graph.microsoft.com/v1.0/subscriptions/
{
    "changeType": "created,updated,deleted",
    "notificationUrl": "https://webhook.azurewebsites.net/api/send/myNotifyClient",
    "resource": "users('1273a016-201d-4f95-8083-1b7f99b3edeb')/events",
    "expirationDateTime": "2022-05-05T14:58:56.7951795+00:00",
    "clientState": "ClientSecret",
    "includeResourceData": false
}
```

アプリは、サブスクライブされた会議イベントについて通知されると、通知でカレンダー イベント ID を探します。 イベント ID を使用して、特定のチャット ID を取得し、そのメッセージをサブスクライブするための `JoinWebUrl` を取得します。 アプリがチャット メッセージをサブスクライブしたら、[テナント レベルの通知](#obtain-meeting-details-using-tenant-level-notification)の手順に従って、会議 ID と開催者 ID を取得します。

ユーザー レベルの通知から会議 ID と開催者 ID を取得するには:

1. **イベント ID を取得する**: アプリは、通知ペイロードから `eventId` プロパティを取得します。

    <details>
    <summary><b>例</b>: 通知ペイロード</summary>

    ```json
    {
        "subscriptionId": "ef30cdc6-b5ae-4702-b924-f458fd9e5fc3",
        "changeType": "created",
        "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
        "clientState": "ClientSecret",
        "subscriptionExpirationDateTime": "2022-05-05T07:54:53.1886542-07:00",
        "resource": "Users/1273a016-201d-4f95-8083-1b7f99b3edeb/Events/AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=",
        "resourceData": {}
    }
    ```

    この例では、`resource` に含まれる `eventID` は *AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=* です。
    </details>

2. **会議 URL を取得する**: イベント ID を使用して、会議 URL を含む `joinUrl` を取得します。

    詳細については、「[イベントの取得](/graph/api/event-get)」を参照してください。

    次の例を使用して、会議 URL を要求します。

    ```http
    GET https://graph.microsoft.com/v1.0/users/1273a016-201d-4f95-8083-1b7f99b3edeb/events/AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=
    ```

    応答ペイロードには `joinURL` が含まれます。

    <details>
    <summary><b>例</b>: 会議 URL を取得するための応答ペイロード</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('1273a016-201d-4f95-8083-1b7f99b3edeb')/events/$entity",
        "@odata.etag": "W/\"xRVh47aDEU6na1ckNYfMiwABb2Twsg==\"",
        "id": "AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=",    
        "start": {
            "dateTime": "2022-05-06T15:00:00.0000000",
            "timeZone": "UTC"
        },
        "end": {
            "dateTime": "2022-05-06T15:30:00.0000000",
            "timeZone": "UTC"
        },
            
        "onlineMeeting": {
            "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MjExYzJiMTItZDY1MS00ZGZkLWE5YzQtZTBmNWI1MDg2M2Uw%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%221273a016-201d-4f95-8083-1b7f99b3edeb%22%7d",
            "conferenceId": "438824583",
            "tollNumber": "+1 213-279-1007"
        }    
    }
    ```

    </details>

    会議 URL は `joinUrl` に含まれています。

3. **チャット スレッド ID を取得する**: `joinUrl` で取得した会議 URL を使用して、チャット スレッド ID を取得します。 関連する会議をフェッチする際に、この会議 URL を `joinWebUrl` パラメーターの値として指定します。

    次の例を使用して、スレッド ID を要求します。

    ``` http
    GET https://graph.microsoft.com/v1.0/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings?$filter=JoinWebUrl%20eq%20'https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d'
    ```

    応答ペイロードには、`chatInfo` プロパティ内の `threadID` メンバーが含まれています。
    <br>
    <details>
    <summary><b>例</b>: スレッド ID を持つ応答ペイロード</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings",
        "value": [
            {
                "id": "MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19NVE01T1RZM01HVXRObVk0TWkwMFlqZzRMVGsyTURVdFkySXlaR1JsTm1VMVpqQTJAdGhyZWFkLnYy",
                "creationDateTime": "2022-04-26T07:41:17.3736455Z",
                "startDateTime": "2022-04-26T10:30:00Z",
                "endDateTime": "2022-04-26T11:00:00Z",
                "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "chatInfo": {
                    "threadId": "19:meeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2@thread.v2",
                    "messageId": "0",
                    "replyChainMessageId": null
                }
            }
        ]
    }
    ```

    </details>

    チャット ID は `threadId` に含まれます。

4. **チャット メッセージをサブスクライブする**: チャット ID を使用してアプリをサブスクライブし、その特定の会議のチャット メッセージを受信します。 詳細については、「[チャットでメッセージをサブスクライブする](/graph/teams-changenotifications-chatmessage#subscribe-to-messages-in-a-chat)」を参照してください。

    アプリで特定のテキストを含むメッセージをサブスクライブする場合は、「[特定のテキストを含むチャットでメッセージをサブスクライブする](/graph/teams-changenotifications-chatmessage#example-2-subscribe-to-messages-in-a-chat-that-contain-certain-text)」を参照してください。

5. [テナント レベルの通知](#obtain-meeting-details-using-tenant-level-notification)の手順に従って、会議 ID と開催者 ID を取得します。

#### <a name="obtain-meeting-details-using-tenant-level-notification"></a>テナント レベルの通知を使用して会議の詳細を取得する

テナント レベルの通知は、アプリがテナント全体のすべての会議トランスクリプトへのアクセスを承認されている場合に役立ちます。 アプリをサブスクライブして、スケジュールされたオンライン Teams 会議のトランスクリプトの開始時または通話の終了時にイベントの通知を受け取ります。 会議の終了後、アプリは会議のトランスクリプトにアクセスして取得できます。

アプリをテナント レベルの通知にサブスクライブするには、「[変更通知を取得する](/graph/teams-changenotifications-chatmessage#subscribe-to-messages-across-all-chats)」を参照してください。

アプリは、サブスクライブされた会議イベントについて通知されると、通知を通じて、トランスクリプトの開始イベントと会議の終了イベントを検索します。 これらのイベントには、チャット エンティティを取得するために使用されるチャット ID が含まれ、最終的には会議 ID と開催者 ID が含まれます。

テナント レベルの通知から会議 ID と開催者 ID を取得するには:

1. **チャット ID を取得する**: アプリは通知から `chatId` プロパティを取得して、後続の呼び出しを行います。 アプリは、次のペイロードからチャット ID を取得できます。

    - トランスクリプト開始イベント: `callTranscriptEventMessageDetail` イベントの種類

        <details>
        <summary><b>例</b>: トランスクリプト開始イベントのペイロード</summary>

        ```json
        {
        "subscriptionId": "1217470f-564c-4fe3-b51f-ebd962cb8797",
        "changeType": "created",
        "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
        "resource": "chats('19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2')/messages('1649787549174')",
        "contentDecryptedBySimulator": {
            "@odata.context": "https://graph.microsoft.com/$metadata#chats('19%3Ameeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk%40thread.v2')/messages/$entity",
            "messageType": "systemEventMessage",
            "createdDateTime": "2022-04-12T18:19:09.174Z",
            "lastModifiedDateTime": "2022-04-12T18:19:09.174Z",
            "chatId": "19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2",
            "body": {
                "contentType": "html",
                "content": "<systemEventMessage/>"
            },
            "channelIdentity": null,
            "eventDetail": {
                "@odata.type": "#Microsoft.Teams.GraphSvc.callTranscriptEventMessageDetail",
                "callId": "16481de8-3262-419b-abc7-0139e6239515",
                "callTranscriptICalUid": "",
                "meetingOrganizer": {
                    "application": null,
                    "device": null,
                    "user": {
                    "userIdentityType": "aadUser",
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null
                        }
                    }
                }
            },
            "encryptedContent": {}
        }
        ```

        </details>

    - 呼び出し終了イベント: `callEndedEventMessageDetail` イベントの種類

        <details>
        <summary><b>例</b>: 呼び出し終了イベントのペイロード</summary>

        ```json
        {
            "subscriptionId": "1217470f-564c-4fe3-b51f-ebd962cb8797",
            "changeType": "created",
            "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
            "resource": "chats('19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2')/messages('1649787585457')",
            "resourceData": {},
            "contentDecryptedBySimulator": {
                "@odata.context": "https://graph.microsoft.com/$metadata#chats('19%3Ameeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk%40thread.v2')/messages/$entity",
                "createdDateTime": "2022-04-12T18:19:45.457Z",
                "lastModifiedDateTime": "2022-04-12T18:19:45.457Z",     
                "chatId": "19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2",
                "eventDetail": {
                    "@odata.type": "#Microsoft.Teams.GraphSvc.callEndedEventMessageDetail",
                    "callId": null,
                    "callDuration": "PT1M44S",
                    "callEventType": "meeting",
                    "callParticipants": [
                    ],
                    "initiator": {
        
                    }
                }
            },
            "encryptedContent": {
                    
            }
        }
        ```

        </details>

2. **チャット エンティティを取得する**: アプリは、手順 1 で取得したチャット ID を使用してチャット エンティティを取得できます。 チャット エンティティを使用して、通話に参加するための URL を取得します。 `onlineMeetingInfo` プロパティの `joinWebUrl` メンバーにはこの URL が含まれており、最終的に会議 ID を取得するために使用されます。 開催者 ID も応答ペイロードの一部です。

    チャット エンティティの詳細については、「[チャットの取得](/graph/api/chat-get)」を参照してください。

    次の例を使用して、チャット ID に基づいてチャット エンティティを要求します。

    ``` http
    GET https://graph.microsoft.com/v1.0/chats/19:meeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2@thread.v2
    ```

    応答ペイロードには、次の要素が含まれています。

    - **開催者 ID**: これは、応答ペイロードの `organizer` プロパティの `id` メンバーに含まれています。
    - **会議呼び出しの URL**: この URL は会議 ID を取得するために使用され、次の 2 つのシナリオのいずれかで応答ペイロードで使用できます。
        - 会議がオンライン Teams 会議の場合、`onlineMeetingInfo` プロパティの `joinWebUrl` メンバーにはこの URL が含まれます。
        - 会議が Teams クライアントまたは Outlook クライアントからオンライン会議として作成されたものではない場合、`onlineMeetingInfo` プロパティに `calendarEventId` メンバーが含まれます。 アプリは `calendarEventId` を使用して `joinUrl` を取得できます。これは `joinWebUrl` と同じです。

      イベントの詳細については、「[イベントの取得](/graph/api/event-get?view=graph-rest-1.0&tabs=http&preserve-view=true)」を参照してください。

      参加会議 URL の種類に応じた応答ペイロード シナリオの例:

        - `joinWebUrl` が利用できるオンライン Teams 会議

            <details>
            <summary><b>例</b>: オンライン会議の応答ペイロード</b></summary>

            ```json
            {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#chats/$entity",
                "id": "19:meeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2@thread.v2",
                "topic": "Test Meet Create Online Meeting",
                "createdDateTime": "2022-04-14T11:30:45.903Z",
                "lastUpdatedDateTime": "2022-04-26T06:27:45.265Z",
                "chatType": "meeting",
                "webUrl": "https://teams.microsoft.com/l/chat/19%3Ameeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2%40thread.v2/0?tenantId=2432b57b-0abd-43db-aa7b-16eadd115d34",
                "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
                "viewpoint": null,
                "onlineMeetingInfo": {
                "calendarEventId": null,
                    "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                    "organizer": {
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null,
                        "userIdentityType": "aadUser"
                    }
                }
            }
            ```

            </details>

        - Teams クライアントまたは Outlook クライアントを通じてスケジュールされた会議で、`calendarEventId` が利用可能なオンライン会議としてマークされていない

            <details>
            <summary><b>例</b>: 会議の応答ペイロードがオンラインとしてマークされていない</summary>

            ```json
            {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#chats/$entity",
                "id": "19:meeting_YzM1NGFiZWYtOGFiOS00NjM5LTg4OTktYmU0MjI4NTQyNGZm@thread.v2",
                "topic": "Non Online Meeting Teams Client",
                "createdDateTime": "2022-04-26T09:43:23.711Z",
                "lastUpdatedDateTime": "2022-04-26T09:43:46.157Z",
                "chatType": "meeting",
                "webUrl": "https://teams.microsoft.com/l/chat/19%3Ameeting_YzM1NGFiZWYtOGFiOS00NjM5LTg4OTktYmU0MjI4NTQyNGZm%40thread.v2/0?tenantId=2432b57b-0abd-43db-aa7b-16eadd115d34",
                "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
                "viewpoint": null,
                "onlineMeetingInfo": {
                    "calendarEventId": "AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYeAAA=",
                    "joinWebUrl": null,
                    "organizer": {
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null,
                        "userIdentityType": "aadUser"
                    }
                }
            }
            ```

            </details>

            - 次の例を使用して、`calendarEventId` から `joinWebUrl` を取得します。

              ``` http
                GET https://graph.microsoft.com/beta/users/14b779ae-cb64-47e7-a512-52fd50a4154d/events/AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYdAAA=
              ```

              この例では次のようになっています。

                - 開催者 ID は *14b779ae-cb64-47e7-a512-52fd50a4154d* です。

              この要求の応答ペイロードには、`onlineMeeting` プロパティに `joinUrl` が含まれています。

                > [!NOTE]
                > `joinUrl` は `joinWebUrl` と同じです。

              <br>
              <details>
              <summary><b>例</b>: 会議に参加するための URL を含む応答ペイロード</summary>

              ```json
              {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/events/$entity",
                "@odata.etag": "W/\"bMMOQZSMbU+4hcmFq11dwAAAkc3Tmw==\"",
                "id": "AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYdAAA=",    
                "start": {
                    "dateTime": "2022-04-26T10:30:00.0000000",
                    "timeZone": "UTC"
                },
                "end": {
                    "dateTime": "2022-04-26T11:00:00.0000000",
                    "timeZone": "UTC"
                },    
                "onlineMeeting": {
                    "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d"
                },
                "calendar@odata.associationLink": "https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/calendars('AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQAuAAAAAAD3AG5jNnlgQJvdCL_KgXJIAQBsww5BlIxtT7iFyYWrXV3AAAAAAAENAAA=')/$ref",
                "calendar@odata.navigationLink": "https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/calendars('AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQAuAAAAAAD3AG5jNnlgQJvdCL_KgXJIAQBsww5BlIxtT7iFyYWrXV3AAAAAAAENAAA=')"
                }
                ```

              </details>

3. **会議 ID を取得する**: これで、アプリは `joinWebUrl` を使用して会議 ID を取得できます。

    次の例を使用して、オンライン会議 ID を要求します。

    ``` http
    GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings?$filter=JoinWebUrl%20eq%20'https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d'
    ```

    応答ペイロードには、`value` プロパティの `id` メンバーに会議 ID が含まれています。
    <br>
    <details>
    <summary><b>例</b>: 会議 ID を含む応答ペイロード</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings",
        "value": [
            {
                "id": "MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19NVE01T1RZM01HVXRObVk0TWkwMFlqZzRMVGsyTURVdFkySXlaR1JsTm1VMVpqQTJAdGhyZWFkLnYy",
                "creationDateTime": "2022-04-26T07:41:17.3736455Z",
                "startDateTime": "2022-04-26T10:30:00Z",
                "endDateTime": "2022-04-26T11:00:00Z",
                "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "chatInfo": {
                    "threadId": "19:meeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2@thread.v2",
                    "messageId": "0",
                    "replyChainMessageId": null
                }
            }
        ]
    }
    ```

    </details>

4. **トランスクリプトのフェッチ**: 手順 2 と 3 で取得した開催者 ID と会議 ID により、アプリはその特定の会議イベントのトランスクリプトをフェッチできます。

    トランスクリプトをフェッチするには、次のことを行う必要があります。

    1. **開催者 ID と会議 ID に基づいてトランスクリプト ID を取得します**。

       次の例を使用して、トランスクリプト ID を要求します。

        ```http
        GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings/('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts
        ```

        この例では次のようになっています。

        - 会議 ID は、`onlineMeetings` の値として含まれています: *MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bW VldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM 1pqWTJAdGhyZWFkLnYy*。
        - 開催者 ID は *14b779ae-cb64-47e7-a512-52fd50a4154d* です。

        応答ペイロードには、`value` プロパティの `id` メンバーの会議 ID と開催者 ID のトランスクリプト ID が含まれています。
        <br>
        <details>
        <summary><b>例</b>: トランスクリプト ID を取得するための応答ペイロード</summary>

        ```json
        {
            "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts",
            "@odata.count": 1,
            "value": [
                {
                    "id": "MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh",
                    "createdDateTime": "2022-04-14T11:34:39.5662792Z"
                }
            ]
        }
        ```

        この例では、トランスクリプト ID は *MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh* です。

        </details>

    1. **トランスクリプト ID に基づいて、会議のトランスクリプトにアクセスして取得します**。

        次の例を使用して、特定の会議のトランスクリプトを `.vtt` 形式で要求します。

        ```http
        GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts('MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh')/content?$format=text/vtt
        ```

        応答ペイロードには、`.vtt` 形式のトランスクリプトが含まれます。

### <a name="use-bot-framework-to-get-meeting-id-and-organizer-id"></a>ボット フレームワークを使用して会議 ID と開催者 ID を取得する

アプリでは、会議 ID と開催者 ID を取得するためにボット フレームワークを使用できます。 ボットは、スケジュールされたすべてのオンライン会議から会議の開始または終了イベントを自動的に受信できます。

次の例を使用して、ボット アプリを使用して会議 ID と開催者 ID を取得します。

```json
GET /v1/meetings/{meetingId}
```

応答ペイロードには次のものが含まれます。

- `details` プロパティの `msGraphResourceId` メンバーの会議 ID。
- `organizer` プロパティの `id` メンバーの開催者 ID。
<br>
<details>
<summary><b>例</b>: 会議の詳細を取得するための応答ペイロード</b></summary>

```json
{
  details: {
    id: "MCMxOTptZWV0aW5nX05XTTFNVEk1TnpNdE5qZ3pNeTAwWVdRNExUaG1PV1F0WlRnM01UQm1PVGczWW1VekB0aHJlYWQudjIjMA==",
    msGraphResourceId: "MSo2NzAyYWZiNi0xMDliLTRjMzItYTE0MS02ZTY1NDY5NTAyYjkqMCoqMTk6bWVldGluZ19OV00xTVRJNU56TXROamd6TXkwMFlXUTRMVGhtT1dRdFpUZzNNVEJtT1RnM1ltVXpAdGhyZWFkLnYy",
    scheduledStartTime: {
    },
    scheduledEndTime: {
    },
    joinUrl: "https://teams.microsoft.com/l/meetup-join/19%3ameeting_NWM1MTI5NzMtNjgzMy00YWQ4LThmOWQtZTg3MTBmOTg3YmUz%40thread.v2/0?context=%7b%22Tid%22%3a%22b3cdf1c8-024a-49e2-a994-f67f830b02f3%22%2c%22Oid%22%3a%226702afb6-109b-4c32-a141-6e65469502b9%22%7d",
    title: "Testing meeting bot 1 - Hun",
    type: "Scheduled",
  },
  conversation: {
    id: "19:meeting_NWM1MTI5NzMtNjgzMy00YWQ4LThmOWQtZTg3MTBmOTg3YmUz@thread.v2",
    isGroup: true,
    conversationType: "groupChat",
  },
  organizer: {
    id: "29:1VZkVr77S3GW_RdAXKrfgFeytpqMegL3tkKvEbwrPqoCVvmqrlKtVrfKWUY7xIM-bZIx4Sq-p1MjdjSZnb5W20w",
    tenantId: "b3cdf1c8-024a-49e2-a994-f67f830b02f3",
    aadObjectId: "6702afb6-109b-4c32-a141-6e65469502b9",
  },
}
```

この例では次のようになっています。

- 会議 ID は `msGraphResourceId` の値として含まれています: *MSo2NzAyYWZiNi0xMDliLTRjMzItYTE0MS02ZTY1NDY5NTAyYjkqMCoqMTk6bWVl dGluZ19OV00xTVRJNU56TXROamd6TXkwMFlXUTRMVGhtT1dRdFpUZzNNVEJtT1RnM 1ltVXpAdGhyZWFkLnYy*。
- 開催者 ID は、`organizer` の `id` の値として含まれています: *29:1VZkVr77S3GW_RdAXKrfgFeytpqMegL3tkKvEbwrPqoCVvmqrlKtVrfKWUY7xIM-bZIx4Sq-p1MjdjSZnb5W20w*。

</details>

アプリが会議 ID と開催者 ID を取得すると、Graph API がトリガーされ、これらの会議の詳細を使用してトランスクリプト コンテンツがフェッチされます。

### <a name="code-samples"></a>コード サンプル

ボット アプリの次のコード サンプルを試すことができます。

| **サンプルの名前** | **説明** | **C#** | **Node.js** |
|----------------|-----------------|--------------|--------------|--------------|
| 会議のトランスクリプト | これは、Graph API を使用してトランスクリプトを取得し、タスク モジュールで表示する方法を示すサンプル アプリケーションです。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-transcription/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-transcription/nodejs) |

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [トランスクリプトをフェッチするための Graph API](/graph/api/resources/calltranscript)
