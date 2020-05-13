---
title: アプリのトラブルシューティング
description: Microsoft Teams 用アプリの作成中に発生する問題やエラーのトラブルシューティング
keywords: teams アプリ開発のトラブルシューティング
ms.date: 07/09/2018
ms.openlocfilehash: 5f6c8b2d5496d1c49ea35b069c16f4ede507f5e1
ms.sourcegitcommit: b9e8839858ea8e9e33fe5e20e14bbe86c75fd510
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "44210709"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>Microsoft Teams アプリのトラブルシューティング

## <a name="troubleshooting-tabs"></a>トラブルシューティングのタブ

### <a name="accessing-the-devtools"></a>DevTools へのアクセス

[Teams クライアントで Devtools](~/tabs/how-to/developer-tools.md)を開くには、ブラウザーで F12 キー (Windows の場合) またはコマンドオプション-I (MacOS) を押した場合と同様の手順を実行します。

### <a name="blank-tab-screen"></a>空白のタブ画面

タブビューにコンテンツが表示されない場合は、次のようになります。

* コンテンツをに表示することはできません `<iframe>` 。
* コンテンツドメインは、マニフェストの[Validdomains](~/resources/schema/manifest-schema.md#validdomains)リストに含まれていません。

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>[設定] ダイアログボックスの [保存] ボタンが有効になっていない

`microsoftTeams.settings.setValidityState(true)`[保存] ボタンを有効にするには、ユーザーが入力したか、または [設定] ページですべての必要なデータを選択した場合には、必ず通話してください。

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a>[保存] ボタンを選択すると、タブの設定を保存できません。

タブを追加するときに、[保存] ボタンをクリックしても、設定を保存できないことを示すエラーメッセージが表示される場合は、次の2つのクラスのいずれかの問題が考えられます。

* 保存成功メッセージは受信されませんでした。 を使用して保存ハンドラーが登録されている場合、 `microsoftTeams.settings.registerOnSaveHandler(handler)` コールバックはを呼び出す必要があり `saveEvent.notifySuccess()` ます。 このエラーは、コールバックが30秒以内に、または `saveEvent.notifyFailure(reason)` その代わりに呼び出しを行わない場合に表示されます。

* 保存ハンドラーが登録されていない場合は、 `saveEvent.notifySuccess()` ユーザーが [保存] ボタンを選択すると、その時点で通話が自動的に実行されます。

* 指定された設定は無効です。 その他の理由として、設定が無効な設定オブジェクトを呼び出した場合、または呼び出しが行われなかった場合は、設定が保存されないことがあり `microsoftTeams.setSettings(settings)` ます。 Settings オブジェクトの一般的な問題については、次のセクションを参照してください。

### <a name="common-problems-with-the-settings-object"></a>Settings オブジェクトの一般的な問題

* `settings.entityId`がありません。 通常、このフィールドには、定義される年ごとに 1 が指定されます。
* `settings.contentUrl`がありません。 通常、このフィールドには、定義される年ごとに 1 が指定されます。
* `settings.contentUrl`またはオプションですが、有効では `settings.removeUrl` `settings.websiteUrl` ありません。 Url は HTTPS を使用する必要があり、また、マニフェストの一覧で指定されているか、または設定ページと同じドメインである必要があり `validDomains` ます。

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>ユーザーを認証できないか、またはタブに認証プロバイダーが表示されない

サイレント認証を実行していない場合は、 [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client.md)によって提供される認証プロセスに従う必要があります。

> [!NOTE]
>すべての認証フローをドメインで開始および終了する必要があり `validDomains` ます。これはマニフェスト内のオブジェクトに記載されている必要があります。

認証の詳細については、「[ユーザーの認証](~/concepts/authentication/authentication.md)」を参照してください。

### <a name="static-tabs-not-showing-up"></a>静的タブが表示されない

新規または更新された静的なタブを使用して既存のボットアプリを更新すると、個人のチャット会話からアプリにアクセスしたときにそのタブの変更が表示されないという既知の問題があります。  変更を確認するには、新しいユーザーまたはテストインスタンスでテストするか、アプリのポップアップから bot にアクセスする必要があります。

## <a name="troubleshooting-bots"></a>ボットのトラブルシューティング

### <a name="cant-add-my-bot"></a>Bot を追加できません

アプリをエンドユーザーが読み込むには、Office 365 テナント管理者が有効にする必要があります。 場合によっては、Office 365 テナントに複数の Sku が関連付けられている可能性があります。また、bot がどのような場合でも機能するには、すべての Sku で有効になっている必要があります。 詳細については[、「Office 365 テナントの準備](~/concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。

### <a name="cant-add-bot-as-a-member-of-a-team"></a>Bot をチームのメンバーとして追加できません

そのチームのチャネル内でアクセスできるようにするには、最初に bot をチームにアップロードする必要があります。 このプロセスの詳細については、「[チームでアプリをアップロードする」](~/concepts/deploy-and-publish/apps-upload.md)を参照してください。

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>自分の bot がチャネルでメッセージを受信できない

チャネル内の bot は、前の bot メッセージに返信する場合でも、明示的に @mentioned ときにのみメッセージを受信します。 メッセージに bot 名が表示されない唯一の例外は、 `imBack` 最初に送信した cardaction の結果として bot がアクションを受け取った場合です。

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>自分の bot がチャネル内で自分のコマンドを理解していない

チャネル内のボットは @mentioned 時にのみメッセージを受信するので、ボットがチャネル内で受信するすべてのメッセージには、テキストフィールドに @mention が含まれます。 解析ロジックに渡す前に、すべての受信テキストメッセージから bot 名自体を削除することをお勧めします。 このケースを処理する方法に関するヒントについては、[メンション](../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions)を確認してください。

## <a name="issues-with-packaging-and-uploading"></a>パッケージ化とアップロードに関する問題

### <a name="error-while-reading-manifestjson"></a>Manifest.xml の読み取り中にエラーが発生しました

ほとんどのマニフェストエラーは、不足している、または無効なフィールドに関するヒントを提供します。 ただし、JSON ファイルを JSON として読み取ることができない場合は、この一般的なエラーメッセージが使用されます。

マニフェストの読み取りエラーの一般的な理由:

* 無効な JSON です。 JSON 構文を自動的に検証する[Visual Studio Code](https://code.visualstudio.com)または[visual STUDIO](https://www.visualstudio.com/vs/)などの IDE を使用します。
* エンコードの問題。 *Manifest.xml*ファイルには、utf-8 を使用します。 その他のエンコーディング (具体的には、BOM を含む) は読み取ることができない場合があります。
* .Zip パッケージの形式が正しくない。 *Manifest.xml*ファイルは、.zip ファイルの最上位レベルにある必要があります。 既定の Mac ファイル圧縮では、*マニフェスト*がサブディレクトリに配置される可能性があることに注意してください。これは、Microsoft Teams に適切に読み込まれません。

### <a name="another-extension-with-same-id-exists"></a>同じ ID を持つ別の内線番号が存在します

同じ ID を持つ更新されたパッケージを再アップロードする場合は、[**アップロード**] ボタンではなく、タブの table 行の最後にある [**置換**] アイコンを選択します。

更新されたパッケージを再アップロードしない場合は、ID が一意であることを確認してください。
