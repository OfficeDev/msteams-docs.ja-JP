---
title: アプリのトラブルシューティング
description: アプリの構築中に問題やエラーをトラブルシューティングMicrosoft Teams
keywords: teams アプリ開発のトラブルシューティング
localization_priority: Normal
ms.topic: troubleshooting
ms.date: 07/09/2018
ms.openlocfilehash: ce45a75869e8b6694cd84c10f8fac1f9bd55bad4
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020430"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>アプリのトラブルシューティングMicrosoft Teamsする

## <a name="troubleshooting-tabs"></a>タブのトラブルシューティング

### <a name="accessing-the-devtools"></a>DevTools へのアクセス

Teams クライアントで[DevTools](~/tabs/how-to/developer-tools.md)を開き、ブラウザーで F12 (on Windows) または Command-Option-I (MacOS 上) を押すのと同様のエクスペリエンスを提供できます。

### <a name="blank-tab-screen"></a>空白のタブ画面

タブ ビューにコンテンツが表示されない場合は、次の可能性があります。

* コンテンツは、 に表示できません `<iframe>` 。
* コンテンツ ドメインがマニフェストの [validDomains リスト](~/resources/schema/manifest-schema.md#validdomains) に含まれています。

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>設定ダイアログで [保存] ボタンが有効になっていない

ユーザーが入力を `microsoftTeams.settings.setValidityState(true)` 受け取った後、または設定ページで必要なすべてのデータを選択して保存ボタンを有効にしたら、必ず呼び出してください。

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a>[保存] ボタンを選択すると、タブ設定を保存できません。

タブを追加するときに、保存ボタンをクリックしたが、設定を保存できないことを示すエラー メッセージが表示された場合、問題は次の 2 つのクラスの 1 つになる可能性があります。

* 成功の保存メッセージは受信されません。 保存ハンドラーが使用して登録されている場合 `microsoftTeams.settings.registerOnSaveHandler(handler)` 、コールバックは呼び出す必要があります `saveEvent.notifySuccess()` 。 コールバックが 30 秒以内にこれを呼び出したり、代わりに呼び出しを行わない場合は、 `saveEvent.notifyFailure(reason)` このエラーが表示されます。

* 保存ハンドラーが登録されていない場合、ユーザーが [保存] ボタンを選択すると、すぐに `saveEvent.notifySuccess()` 呼び出しが自動的に行われます。

* 指定された設定が無効でした。 設定を保存できないもう 1 つの理由は、呼び出しが無効な設定オブジェクトを提供した場合、または呼び出しが行われた `microsoftTeams.setSettings(settings)` のではない場合です。 次のセクション「settings オブジェクトに関する一般的な問題」を参照してください。

### <a name="common-problems-with-the-settings-object"></a>settings オブジェクトに関する一般的な問題

* `settings.entityId` が見つからない。 通常、このフィールドには、定義される年ごとに 1 が指定されます。
* `settings.contentUrl` が見つからない。 通常、このフィールドには、定義される年ごとに 1 が指定されます。
* `settings.contentUrl` または省略可能 `settings.removeUrl` な 、 `settings.websiteUrl` または指定されているが無効です。 URL は HTTPS を使用する必要があります。また、設定ページと同じドメインか、マニフェストの一覧で指定する必要 `validDomains` があります。

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>ユーザーを認証できない、またはタブに認証プロバイダーを表示できない

サイレント認証を行う場合をしない限り、JavaScript クライアント SDK で提供される認証[Microsoft Teams実行する必要があります](/javascript/api/overview/msteams-client.md)。

> [!NOTE]
>ドメインで開始および終了するには、すべての認証フローが必要です。これはマニフェストのオブジェクトに一 `validDomains` 覧表示する必要があります。

認証の詳細については、「ユーザーの認証 [」を参照してください](~/concepts/authentication/authentication.md)。

### <a name="static-tabs-not-showing-up"></a>静的タブが表示されない

新しい静的タブまたは更新された静的タブを使用して既存のボット アプリを更新すると、個人のチャット会話からアプリにアクセスするときにタブの変更が表示されないという既知の問題があります。  変更を確認するには、新しいユーザーまたはテスト インスタンスでテストするか、アプリ のフライアウトからボットにアクセスする必要があります。

## <a name="troubleshooting-bots"></a>ボットのトラブルシューティング

### <a name="cant-add-my-bot"></a>ボットを追加できない

エンド ユーザーが読み込むには、Office 365テナント管理者がアプリを有効にする必要があります。 場合によっては、Office 365 テナントに複数の SKU が関連付けられている可能性があります。ボットが任意で動作するには、すべての SKU で有効にする必要があります。 詳細については[、「prepare your Office 365 テナント](~/concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。

### <a name="cant-add-bot-as-a-member-of-a-team"></a>チームのメンバーとしてボットを追加できない

ボットは、そのチームのチャネル内でアクセスできる前に、まずチームにアップロードする必要があります。 このプロセス [の詳細については、「チームでのアプリのアップロード](~/concepts/deploy-and-publish/apps-upload.md) 」を参照してください。

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>ボットがチャネルでメッセージを受け取らない

チャネル内のボットは、以前のボット メッセージに返信している場合@mentionedメッセージを明示的に受信した場合にのみメッセージを受信します。 メッセージにボット名が表示されない唯一の例外は、ボットが最初に送信した CardAction の結果としてアクションを受信 `imBack` した場合です。

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>チャネルで自分のコマンドをボットが理解していない

チャネル内のボットはメッセージを受信する@mentioned、チャネルで受信するメッセージはすべてテキスト フィールドに@mention含まれます。 解析ロジックに渡す前に、ボット名自体をすべての受信テキスト メッセージから取り除くのがベスト プラクティスです。 この [ケースを処理](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) する方法に関するヒントについては、メンションを確認してください。

## <a name="issues-with-packaging-and-uploading"></a>パッケージ化とアップロードに関する問題

### <a name="error-while-reading-manifestjson"></a>読み取り中のエラーmanifest.jsオン

ほとんどのマニフェスト エラーは、特定のフィールドが見つからないか無効かを示すヒントを提供します。 ただし、JSON ファイルを JSON として全く読み取りできない場合は、この汎用エラー メッセージが使用されます。

マニフェストの読み取りエラーの一般的な理由:

* JSON が無効です。 JSON 構文を自動的に検証[する](https://code.visualstudio.com)[Visual Studio CodeまたはVisual Studio](https://www.visualstudio.com/vs/) IDE を使用します。
* エンコードの問題。 ファイルUTF-8にmanifest.js *を使用* します。 その他のエンコード (特に BOM を使用) は読み取り可能ではない場合があります。
* 不正な形式.zipパッケージ。 ファイル *manifest.jsは* 、ファイルのトップ レベルにある.zipがあります。 既定の Mac ファイル圧縮では、サブディレクトリにmanifest.jsがオンになる場合があり、このファイルは正しく読み込まれMicrosoft Teams。

### <a name="another-extension-with-same-id-exists"></a>同じ ID を持つ別の拡張機能が存在する

同じ ID で更新されたパッケージを再アップロードする場合は、タブのテーブル行の末尾にある [置換] アイコンを [アップロード] ボタン **ではなく選択します**。

更新されたパッケージを再アップロードしない場合は、ID が一意である必要があります。
