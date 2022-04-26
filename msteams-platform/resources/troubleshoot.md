---
title: アプリのトラブルシューティング
description: Microsoft Teams 用アプリのビルド中の問題またはエラーのトラブルシューティング
keywords: teams アプリ開発のトラブルシューティング
localization_priority: Normal
ms.topic: troubleshooting
ms.date: 07/09/2018
ms.openlocfilehash: 9688f2023707ca4eb3e7de6b52d3395a4cba47fd36dd29599dc4ead590368b95
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57708039"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>Microsoft Teams アプリのトラブルシューティング

## <a name="troubleshooting-tabs"></a>タブのトラブルシューティング

### <a name="accessing-the-devtools"></a>DevTools へのアクセス

[Teams クライアントで DevTools](~/tabs/how-to/developer-tools.md) を開くと、ブラウザーで F12 キー (Windows 上) キーまたは Command-Option-I キー (MacOS 上) キーを押すのと同様の操作を行うことができます。

### <a name="blank-tab-screen"></a>空白のタブ画面

タブ ビューにコンテンツが表示されない場合は、次のようになります。

* お使いのコンテンツを `<iframe>` 内に表示できません。
* コンテンツ ドメインがマニフェストの [validDomains](~/resources/schema/manifest-schema.md#validdomains) の一覧にありません。

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>[設定] ダイアログで [保存] ボタンが有効になっていない

ユーザーが設定ページで必要なすべてのデータを入力または選択したら、必ず `microsoftTeams.settings.setValidityState(true)` を呼び出して保存ボタンを有効にしてください。

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a>[保存] ボタンを選択した後、タブ設定を保存できません

タブを追加するときに、 [保存] ボタンをクリックしても設定を保存できないことを示すエラー メッセージが表示された場合、問題は次の 2 つのクラスの問題のいずれかである可能性があります。

* 保存成功メッセージが受信されませんでした。 保存ハンドラーが `microsoftTeams.settings.registerOnSaveHandler(handler)` を使用して登録されている場合は、コールバックは、 `saveEvent.notifySuccess()` を呼び出す必要があります。 コールバックが 30 秒以内にこれを呼び出さない場合や、代わりに `saveEvent.notifyFailure(reason)` の呼び出しを行わない場合は、このエラーが表示されます。

* 保存ハンドラーが登録されていない場合は、ユーザーが保存ボタンを選択すると、すぐに `saveEvent.notifySuccess()` の呼び出しが自動的に行われます。

* 指定された設定が無効でした。 設定を保存できないもう 1 つの理由は、 `microsoftTeams.setSettings(settings)` の呼び出しで無効な設定オブジェクトを指定した場合、または呼び出しがまったく行われなかった場合です。 次のセクションの「設定オブジェクトに関する一般的な問題」を参照してください。

### <a name="common-problems-with-the-settings-object"></a>設定オブジェクトに関する一般的な問題

* `settings.entityId` が見つかりません。 通常、このフィールドには、定義される年ごとに 1 が指定されます。
* `settings.contentUrl` が見つかりません。 通常、このフィールドには、定義される年ごとに 1 が指定されます。
* `settings.contentUrl` または省略可能な `settings.removeUrl`、または `settings.websiteUrl` が指定されていますが無効です。 URL は HTTPS を使用する必要があります。また、設定ページと同じドメインであるか、マニフェストの `validDomains` 一覧で指定されている必要があります。

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>ユーザーを認証できない、またはタブに認証プロバイダーを表示できない

サイレント認証を行っている場合を除き、 [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client.md) によって提供される認証プロセスに従う必要があります。

> [!NOTE]
>すべての認証フローをドメインで開始および終了する必要があります。このフローは、マニフェストの `validDomains` オブジェクトに一覧表示する必要があります。

認証の詳細については、「[ユーザーの認証](~/concepts/authentication/authentication.md)」を参照してください。

### <a name="static-tabs-not-showing-up"></a>静的タブが表示されない

新しいタブまたは更新された静的タブで既存のボット アプリを更新しても、個人用チャット会話からアプリにアクセスするときにタブの変更が表示されないという既知の問題があります。  変更を確認するには、新しいユーザーまたはテスト インスタンスでテストするか、アプリ ポップアップからボットにアクセスする必要があります。

## <a name="troubleshooting-bots"></a>ボットのトラブルシューティング

### <a name="cant-add-my-bot"></a>ボットを追加できない

エンド ユーザーがアプリを読み込むには、 Office 365 テナント管理者がアプリを有効にする必要があります。 場合によっては、 Office 365 テナントに複数の SKU が関連付けられている場合があり、ボットがいずれかの SKU で動作するには、すべての SKU で有効にする必要があることに注意してください。 詳細については、「[Office 365 テナントの準備](~/concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。

### <a name="cant-add-bot-as-a-member-of-a-team"></a>チームのメンバーとしてボットを追加できない

ボットは、そのチームの任意のチャネル内でアクセスできるようになる前に、まずチームにアップロードする必要があります。 このプロセスの詳細については、 「[チームでのアプリのアップロード](~/concepts/deploy-and-publish/apps-upload.md)」に関するページを参照してください。

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>ボットでチャネルにメッセージが表示されない

チャネル内のボットは、前のボット メッセージに返信している場合でも、メッセージが明示的に @mentioned されている場合にのみメッセージを受信します。 メッセージにボット名が表示されない唯一の例外は、ボットが最初に送信した CardAction の結果として `imBack` アクションを受け取った場合です。

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>チャネル内で自分のコマンドがボットで認識されない

チャネル内のボットは @mentioned された場合にのみメッセージを受信するため、ボットがチャネルで受信するすべてのメッセージには、テキスト フィールドにその @mention が含まれます。 解析ロジックに渡す前に、ボット名自体をすべての受信テキスト メッセージから取り除くことがベスト プラクティスです。 このケースを処理する方法に関するヒントについては、「[メンション](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)」を確認してください。

## <a name="issues-with-packaging-and-uploading"></a>パッケージ化とアップロードに関する問題

### <a name="error-while-reading-manifestjson"></a>manifest.json の読み取り中にエラーが発生しました

ほとんどのマニフェスト エラーは、特定のフィールドが見つからないか無効かを示すヒントを提供します。 ただし、 JSON ファイルを JSON としてまったく読み取ることができない場合は、この汎用エラー メッセージが使用されます。

マニフェスト読み取りエラーの一般的な理由:

* JSON が無効です。 JSON 構文を自動的に検証する [Visual Studio Code](https://code.visualstudio.com) や [Visual Studio](https://www.visualstudio.com/vs/) などの IDE を使用します。
* エンコードの問題。 *manifest.json* ファイルには UTF-8 を使用します。 その他のエンコードは、特に BOM では読み取れない場合があります。
* 形式が正しくない .zip パッケージ。 *manifest.json* ファイルは、 .zip ファイルの最上位レベルにある必要があります。 既定の Mac ファイル圧縮では、 *manifest.json* がサブディレクトリに配置され、 Microsoft Teams に正しく読み込まれない可能性があることに注意してください。

### <a name="another-extension-with-same-id-exists"></a>同じ ID を持つ別の拡張機能が存在する

同じ ID で更新されたパッケージを再アップロードする場合は、 **[アップロード]** ボタンではなくタブのテーブル行の末尾にある **[置換]** アイコンを選択します。

更新されたパッケージを再アップロードしない場合は、 ID が一意であることを確認します。
