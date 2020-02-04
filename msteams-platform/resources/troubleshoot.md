---
title: アプリのトラブルシューティング
description: Microsoft Teams 用アプリの作成中に発生する問題やエラーのトラブルシューティング
keywords: teams アプリ開発のトラブルシューティング
ms.date: 07/09/2018
ms.openlocfilehash: f7fe42e7c1f3ff2c4d8d1cbe81ed8f71e6c04384
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674646"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>Microsoft Teams アプリのトラブルシューティング

## <a name="troubleshooting-tabs"></a>トラブルシューティングのタブ

### <a name="accessing-the-devtools"></a>DevTools へのアクセス

[Teams クライアントで Devtools](~/tabs/how-to/developer-tools.md)を開くには、ブラウザーで F12 キー (Windows の場合) またはコマンドオプション-I (MacOS) を押した場合と同様の手順を実行します。

### <a name="blank-tab-screen"></a>空白のタブ画面

タブビューにコンテンツが表示されない場合は、次のようになります。

* コンテンツをに表示することは`<iframe>`できません。
* コンテンツドメインは、マニフェストの[Validdomains](~/resources/schema/manifest-schema.md#validdomains)リストに含まれていません。

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>[設定] ダイアログボックスの [保存] ボタンが有効になっていない

[保存] ボタン`microsoftTeams.settings.setValidityState(true)`を有効にするには、ユーザーが入力したか、または [設定] ページですべての必要なデータを選択した場合には、必ず通話してください。

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a>[保存] ボタンを選択すると、タブの設定を保存できません。

タブを追加するときに、[保存] ボタンをクリックしても、設定を保存できないことを示すエラーメッセージが表示される場合は、次の2つのクラスのいずれかの問題が考えられます。

* 保存成功メッセージは受信されませんでした。 を使用して保存ハンドラーが`microsoftTeams.settings.registerOnSaveHandler(handler)`登録されている`saveEvent.notifySuccess()`場合、コールバックはを呼び出す必要があります。 このエラーは、コールバックが30秒以内に`saveEvent.notifyFailure(reason)` 、またはその代わりに呼び出しを行わない場合に表示されます。

* 保存ハンドラーが登録されてい`saveEvent.notifySuccess()`ない場合は、ユーザーが [保存] ボタンを選択すると、その時点で通話が自動的に実行されます。

* 指定された設定は無効です。 その他の理由として、設定が無効な設定オブジェクト`microsoftTeams.setSettings(settings)`を呼び出した場合、または呼び出しが行われなかった場合は、設定が保存されないことがあります。 Settings オブジェクトの一般的な問題については、次のセクションを参照してください。

### <a name="common-problems-with-the-settings-object"></a>Settings オブジェクトの一般的な問題

* `settings.entityId`がありません。 通常、このフィールドには、定義される年ごとに 1 が指定されます。
* `settings.contentUrl`がありません。 通常、このフィールドには、定義される年ごとに 1 が指定されます。
* `settings.contentUrl`またはオプション`settings.removeUrl` `settings.websiteUrl`ですが、有効ではありません。 Url は HTTPS を使用する必要があり、また、マニフェストの`validDomains`一覧で指定されているか、または設定ページと同じドメインである必要があります。

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>ユーザーを認証できないか、またはタブに認証プロバイダーが表示されない

サイレント認証を実行していない場合は、 [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client.md)によって提供される認証プロセスに従う必要があります。

> [!NOTE]
>すべての認証フローをドメインで開始および終了する必要があります。これはマニフェスト`validDomains`内のオブジェクトに記載されている必要があります。

認証の詳細については、「[ユーザーの認証](~/concepts/authentication/authentication.md)」を参照してください。

### <a name="static-tabs-not-showing-up"></a>静的タブが表示されない

新規または更新された静的なタブを使用して既存のボットアプリを更新すると、個人のチャット会話からアプリにアクセスしたときにそのタブの変更が表示されないという既知の問題があります。  変更を確認するには、新しいユーザーまたはテストインスタンスでテストするか、アプリのポップアップから bot にアクセスする必要があります。

## <a name="troubleshooting-bots"></a>ボットのトラブルシューティング

### <a name="cant-add-my-bot"></a>Bot を追加できません

アプリをエンドユーザーが読み込むには、Office 365 テナント管理者が有効にする必要があります。 場合によっては、Office 365 テナントに複数の Sku が関連付けられている可能性があります。また、bot がどのような場合でも機能するには、すべての Sku で有効になっている必要があります。 詳細については[、「Office 365 テナントの準備](~/concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。

### <a name="cant-add-bot-as-a-member-of-a-team"></a>Bot をチームのメンバーとして追加できません

そのチームのチャネル内でアクセスできるようにするには、最初に bot をチームにアップロードする必要があります。 このプロセスの詳細については、「[チームでアプリをアップロードする」](~/concepts/deploy-and-publish/apps-upload.md)を参照してください。

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>自分の bot がチャネルでメッセージを受信できない

チャネル内の bot は、前の bot メッセージに返信する場合でも、明示的に @mentioned ときにのみメッセージを受信します。 メッセージに bot 名が表示されない唯一の例外は、最初に送信した CardAction の結果として bot が`imBack`アクションを受け取った場合です。

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>自分の bot がチャネル内で自分のコマンドを理解していない

チャネル内のボットは @mentioned 時にのみメッセージを受信するので、ボットがチャネル内で受信するすべてのメッセージには、テキストフィールドに @mention が含まれます。 解析ロジックに渡す前に、すべての受信テキストメッセージから bot 名自体を削除することをお勧めします。 このケースを処理する方法に関するヒントについては、[メンション](~/bots/how-to/conversations/channel-and-group-conversations.md#working-with--mentions)を確認してください。

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
