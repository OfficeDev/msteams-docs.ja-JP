---
title: アプリのトラブルシューティング
description: Microsoft Teams 用アプリのビルド中の問題またはエラーのトラブルシューティング
keywords: teams アプリ開発のトラブルシューティング
localization_priority: Normal
ms.topic: troubleshooting
ms.date: 07/09/2018
ms.openlocfilehash: 76a1a4d45757dff36d45c73f1ea5f2791fbe2e02
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032824"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>Microsoft Teams アプリのトラブルシューティング

## <a name="troubleshooting-tabs"></a>タブのトラブルシューティング

### <a name="accessing-the-devtools"></a>DevTools へのアクセス

[Teams クライアントで DevTools](~/tabs/how-to/developer-tools.md) を開くと、ブラウザーで F12 キー (Windows 上) キーまたは Command-Option-I キー (MacOS 上) キーを押すのと同様の操作を行うことができます。

### <a name="blank-tab-screen"></a>空白のタブ画面

タブ ビューにコンテンツが表示されない場合は、次のようになります。

* コンテンツを .`<iframe>`
* コンテンツ ドメインがマニフェストの [validDomains](~/resources/schema/manifest-schema.md#validdomains) リストにありません。

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>[設定] ダイアログで [保存] ボタンが有効になっていない

ユーザーが設定ページで必要なすべてのデータを入力または選択したら、必ず `microsoftTeams.settings.setValidityState(true)` を呼び出して保存ボタンを有効にしてください。

### <a name="the-tab-settings-cant-be-saved-on-selecting-save"></a>[保存] を選択すると、タブ設定を保存できません

タブを追加するときに、[ **保存]** を選択しても設定を保存できないことを示すエラー メッセージが表示される場合、問題は次の 2 つのクラスの問題のいずれかである可能性があります。

* **保存の成功メッセージが受信されませんでした**。保存ハンドラーが使用して `microsoftTeams.settings.registerOnSaveHandler(handler)`登録されている場合は、コールバックを呼び出す `saveEvent.notifySuccess()`必要があります。

  * コールバックが 30 秒以内に呼び出 `saveEvent.notifySuccess()` されない場合、または代わりに呼び出しが行 `saveEvent.notifyFailure(reason)` われると、このエラーが表示されます。
  * 保存ハンドラーが登録されていない場合、 `saveEvent.notifySuccess()` ユーザーが **[保存**] を選択すると、呼び出しが自動的に行われます。

* **指定された設定が無効でした**。設定が保存されないもう 1 つの理由は、呼び出しが無効な設定オブジェクトを `microsoftTeams.setSettings(settings)` 指定した場合、または呼び出しがまったく行われなかった場合です。 次のセクションの「設定オブジェクトに関する一般的な問題」を参照してください。

### <a name="common-problems-with-the-settings-object"></a>設定オブジェクトに関する一般的な問題

* `settings.entityId` が見つかりません。 通常、このフィールドには、定義される年ごとに 1 が指定されます。
* `settings.contentUrl` が見つかりません。 通常、このフィールドには、定義される年ごとに 1 が指定されます。
* `settings.contentUrl` または省略可能な `settings.removeUrl`、または `settings.websiteUrl` が指定されていますが無効です。 URL は HTTPS を使用する必要があります。また、設定ページと同じドメインであるか、マニフェストの `validDomains` 一覧で指定されている必要があります。

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>ユーザーを認証できない、またはタブに認証プロバイダーを表示できない

サイレント認証を行う場合を除き、[Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) によって提供される認証プロセスに従う必要があります。

> [!NOTE]
>すべての認証フローをドメインで開始および終了する必要があります。このフローは、マニフェストの `validDomains` オブジェクトに一覧表示する必要があります。

認証の詳細については、「 [ユーザーの認証」を参照してください](~/concepts/authentication/authentication.md)。

### <a name="static-tabs-not-showing-up"></a>静的タブが表示されない

既存のボット アプリを新しいタブまたは更新された静的タブで更新しても、個人用チャット会話からアプリにアクセスするときにタブが変更されないという既知の問題があります。  変更を確認するには、新しいユーザーまたはテスト インスタンスでテストするか、アプリ ポップアップからボットにアクセスする必要があります。

## <a name="troubleshooting-bots"></a>ボットのトラブルシューティング

### <a name="cant-add-my-bot"></a>ボットを追加できない

エンド ユーザーがアプリを読み込むには、 Office 365 テナント管理者がアプリを有効にする必要があります。 場合によっては、Office 365 テナントに複数の SKU が関連付けられている場合があり、ボットが任意で動作するには、すべての SKU で有効にする必要があります。 詳細については、「[Office 365 テナントを準備する](~/concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。

### <a name="cant-add-bot-as-a-member-of-a-team"></a>チームのメンバーとしてボットを追加できない

ボットは、そのチームの任意のチャネル内でアクセスできるようにする前に、まずチームにアップロードする必要があります。 このプロセスの詳細については、「 [チームでのアプリのアップロード](~/concepts/deploy-and-publish/apps-upload.md)」を参照してください。

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>ボットでチャネルにメッセージが表示されない

チャネル内のボットは、前のボット メッセージに返信している場合でも、メッセージが明示的に@mentionedされている場合にのみメッセージを受信します。 メッセージにボット名が表示されない唯一の例外は、ボットが最初に送信した CardAction の結果として `imBack` アクションを受け取った場合です。

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>チャネル内で自分のコマンドがボットで認識されない

チャネル内のボットは@mentioned時にのみメッセージを受信するため、チャネルでボットが受信するすべてのメッセージには、テキスト フィールドにその@mentionが含まれます。 解析ロジックに渡す前に、ボット名自体をすべての受信テキスト メッセージから取り除くのがベスト プラクティスです。 このケースを処理する方法に関するヒントについては、「[メンション](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)」を確認してください。

## <a name="issues-with-packaging-and-uploading"></a>パッケージ化とアップロードに関する問題

### <a name="error-while-reading-manifestjson"></a>manifest.json の読み取り中にエラーが発生しました

ほとんどのマニフェスト エラーは、特定のフィールドが見つからないか無効かを示すヒントを提供します。 ただし、JSON ファイルを JSON としてまったく読み取ることができない場合は、この汎用エラー メッセージが使用されます。

マニフェスト読み取りエラーの一般的な理由:

* JSON が無効です。 JSON 構文を自動的に検証する [Visual Studio Code](https://code.visualstudio.com) や [Visual Studio](https://www.visualstudio.com/vs/) などの IDE を使用します。
* エンコードの問題。 *manifest.json* ファイルには UTF-8 を使用します。 その他のエンコードは、特に BOM では読み取れない場合があります。
* 形式が正しくない .zip パッケージ。 *manifest.json* ファイルは、 .zip ファイルの最上位レベルにある必要があります。 既定の Mac ファイル圧縮では *、manifest.json* がサブディレクトリに配置され、Microsoft Teamsに正しく読み込まれない場合があることに注意してください。

### <a name="another-extension-with-same-id-exists"></a>同じ ID を持つ別の拡張機能が存在する

更新されたパッケージを同じ ID で再度アップロードする場合は、タブのテーブル行の末尾にある **[置換**] アイコンを **アップロード** ボタンではなく選択します。

更新されたパッケージを再アップロードしない場合は、 ID が一意であることを確認します。
