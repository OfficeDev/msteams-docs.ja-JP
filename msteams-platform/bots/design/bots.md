---
title: Bot の設計
description: Teams bot を設計し、Microsoft Teams UI キットを取得する方法について説明します。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d1a7470f4986de22ecca7071823b620cb0234abb
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605494"
---
# <a name="designing-your-microsoft-teams-bot"></a>Microsoft Teams bot の設計

Bot は、特定のタスクセットを実行する会話アプリです。 Bot は、 <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot フレームワーク</a>に基づいてユーザーと通信し、質問に応答して、変更やその他のイベントについて事前に通知します。 これらは、お客に到達するための最適な方法です。

アプリの設計をガイドするには、次の情報を参照してください。 Teams でボットを追加、使用、管理する方法について説明しています。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI キットでは、必要に応じて取得および変更できる要素を含む、より包括的な bot 設計ガイドラインを見つけることができます。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を取得する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a>Bot を追加する

Bot は、チャット、チャネル、および個人用アプリで利用できます。 Bot を追加するには、次のいずれかの方法を使用します。

* Teams ストア (AppSource) から。
* Teams の左側にある [ **その他** ] アイコンを選択して、アプリのポップアップを使用します。
* 新しいチャットまたは新規作成ボックスに @mention します (次の例は、グループチャットでこの操作を実行する方法を示しています)。

:::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="例は、@mention を使用してグループチャットに bot を追加する方法を示しています。" border="false":::

## <a name="introduce-a-bot"></a>Bot を導入する

Bot が自らを導入し、その機能について説明していることが重要です。 この最初の exchange は、ユーザーが bot との関係を理解し、制限事項を確認します。

### <a name="welcome-message-in-a-one-on-one-chat"></a>ワンワンチャットでのウェルカムメッセージ

個人のコンテキストでは、ウェルカムメッセージに bot の雰囲気が設定されます。 メッセージには、案内応答、bot が実行できること、および操作方法に関するいくつかの提案が含まれています (たとえば、「質問してください...」)。 可能であれば、これらの提案は、サインインせずに、保存された応答を返す必要があります。

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="例は、個人アプリでの bot の紹介を示しています。" border="false":::

### <a name="introductions-in-group-chats-and-channels"></a>グループチャットとチャネルでの紹介

Bot の紹介は、個人のコンテキスト (個人のアプリなど) と比較して、グループのチャットとチャネルにおいて少し異なるものにする必要があります。 実際には、入室したチャットルームがある場合は、「人」と入力します。既にあるすべてのユーザーを歓迎するのではなく、自分で紹介します。 Bot 設計に対してそのような考えを行います。

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="例は、共同作業コンテキストでの bot の紹介を示しています。" border="false":::

### <a name="bot-authentication-with-single-sign-on"></a>シングルサインオンを使用した Bot 認証

ユーザーが bot にメッセージを送信すると、サインインが必要になる場合があります。そのすべての機能を使用します。 シングルサインオン (SSO) を使用して認証プロセスを簡略化できます。

忘れることはありません。 bot のコマンドメニュー (**何ができますか**) で、サインアウトするコマンドも提供する必要があります。

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="例は、[サインイン] ボタンがある bot を示しています。" border="false":::

### <a name="tours"></a>ガイド

ウェルカムメッセージにツアーを含めることができます。また、bot が "help" コマンドのように応答します。 ツアーは、bot が実行できることを理解するための最も効果的な方法です。 また、必要に応じて、アプリのその他の機能 (たとえば、メッセージング内線番号のスクリーンショットを含む) を記述するのにも適しています。

> [!IMPORTANT]
> ツアーは、サインインしなくてもアクセス可能である必要があります。

#### <a name="one-on-one-chats"></a>1対1のチャット

個人アプリでは、カルーセルを使用して、ボットとアプリのその他の機能の効果的な概要を得ることができます。 ボタンを含む [ユーザーに **タスクを実行する**] コマンドを使用することをお勧めします。

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="例は、1対1のチャットでの bot ツアーを示しています。" border="false":::

#### <a name="channels-and-group-chats"></a>チャネルとグループのチャット

チャネルおよびグループチャットでは、進行中の会話を中断しないように、ツアーはモーダル ( [タスクモジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) とも呼ばれます) で開きます。 これにより、ツアーの役割ベースのビューを実装するオプションも提供されます。

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="例は、チャネル内の bot ツアーを示しています。" border="false":::

## <a name="chat-with-a-bot"></a>Bot とのチャット

Bot は、チームのメッセージングフレームワークに直接統合されます。 ユーザーは bot とチャットすることで、疑問を解決したり、コマンドを入力して、小または特定の一連のタスクを実行したりすることができます。 Bot は、チャット経由でアプリの変更や更新に関するユーザーに積極的な通知を行うことができます。

### <a name="chat-with-a-bot-in-different-contexts"></a>異なるコンテキストにある bot とのチャット

Bot は、次のコンテキストで使用できます。

* **個人アプリ**: 個人アプリでは、ボットには専用のチャットタブがあります。
* **ワンワンチャット**: ユーザーはボットでプライベート会話を開始できます。 個人アプリで bot を使用した場合と同じです。
* **グループチャット**: ユーザーは bot を @mentioning ことで、グループチャットの bot と対話できます。
* **チャネル**: ユーザーはチャネル内の bot と対話できます。 [新規作成] ボックスに bot 名を @mentioning します。 このコンテキストでは、ボットはチャネルだけでなく、チーム全体で利用可能であることに注意してください。

### <a name="anatomy"></a>構造

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="例は、bot の構造的な構造を示しています。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリの名前とアイコン**|
|2 |**[チャット] タブ**: bot と会話するためのスペースを開きます (個人アプリにのみ適用されます)。|
|3 |**カスタムタブ**: アプリに関連するその他のコンテンツを開きます。|
|4 |**[バージョン情報] タブ**: アプリに関する基本情報が表示されます。|
|5 |**チャットバブル**: ボット会話は Teams メッセージングフレームワークを使用します。|
|6 |**アダプティブカード**: bot の応答に適応カードが含まれている場合、カードはチャットのバブルの幅全体を占めます。|
|7 |**コマンドメニュー**: bot の標準コマンド (ユーザーが定義) を表示します。

### <a name="command-menu"></a>コマンドメニュー

コマンドメニューには、ボットに常に応答する単語または語句の一覧が表示されます。 ユーザーが bot に conversing ている場合は、[新規作成] ボックスの上にコマンドメニューが表示されます。 コマンドが選択されている場合は、メッセージに挿入します。

コマンドの一覧は、短くする必要があります。 このメニューは、bot の主要な機能を強調表示することのみを目的としています。 コマンドは簡潔にしてください。 たとえば **、ヘルプというコマンド** を **作成します。**
[コマンド] メニューは、会話の状態に関係なく、常に使用できるようにする必要があります。

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="例は bot のコマンドメニューを示しています。" border="false":::

## <a name="understand-what-people-are-saying"></a>ユーザーが何を言っているかを理解する

シソーラスを使用して、標準クエリのさまざまな解釈を生成できるように、できるだけ多くの背景からユーザーを取得します。

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="Bot が ' Hello ' を解釈する方法を示す図" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="Bot が ' Help ' を解釈する方法を示す図" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="Bot が ' 感謝 ' を解釈する方法を示す図" border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a>メッセージから意図的およびデータを抽出する

意図を認識するように bot を設計し、メッセージまたはクエリに対する応答で bot からの要望を取得します。 インテントは、メッセージまたはクエリを、アクションによって影響を受ける1つ以上のデータオブジェクトを使用して1つのアクションとして分類します。 

次の例は、ボットに送信されたメッセージのユーザーの意図とデータの概要を示しています。

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="「シアトルへのフライトを予約する」という文の例では、ユーザーの目的は「予約」で、データは「シアトル」です。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="例は、「ストアを開いている場合」という文で示されています。ユーザーの意図は ' when ' で、データが ' open ' です。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="「1pm での会議の予約」という文の表示例、ユーザーの目的は ' 1pm ' と ' Bob in Distribution ' のようになっています。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a>分析と改善

ユーザーが bot とチャットするときに読み上げられる内容について説明します。 これは、ユーザーベースがさまざまな場所および orgs で増加している間、継続的に反復的なプロセスになります。 Bot の言語認識と意図的なマッピングを Microsoft 言語理解 (LUIS) で調整することができます。

* [LUIS につい](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence)て: LUIS が AI を使用してアプリデータに自然言語の理解 (nlu) を提供する方法について説明します。
* [LUIS との統合](https://www.luis.ai/): コンピューター学習モデルを作成する複雑なプロセスを使用せずに、bot に自然言語機能を追加します。

## <a name="use-cases"></a>ユース ケース

### <a name="simple-queries"></a>単純なクエリ

Bot は、あいまいさを解決するために、クエリまたは関連する一連の一致項目のグループに正確に一致するものを提供できます。 一致するものがある場合は、リストカードを使用してコンテンツをグループ化します。

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="例は、bot との簡単なクエリ操作を示しています。" border="false":::

### <a name="multi-turn-interactions"></a>複数ターンの相互作用

Bot は完全な要求と質問をサポートできますが、複数ターンの対話を処理できる必要があります。 考えられる次の手順により、ユーザーは、包括的な要求を作成することを期待するのではなく、完全なタスクフローを行うことが容易になります。

次の例では、bot は、次に実行する必要のあるオプションを使用して、各メッセージに応答します。

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="例は、ボットとの相互作用を示しています。" border="false":::

### <a name="reach-out-to-users"></a>ユーザーに連絡する

事前メッセージングでは、bot は、個人、グループチャット、またはチャネルに関連する通知を特定の頻度で送信するダイジェストとして機能することができます。 文書内の内容が変更されたとき、または作業項目が閉じられたときに、bot がメッセージを送信することがあります。

次の例では、ユーザーは、bot が別のチャネルで伝達したトースト通知を取得します。

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="例は、bot が別のチャネルからユーザーに対して事前にメッセージングを行うことを示しています。" border="false":::

これで、そのチャネルでユーザーは bot から自分のメッセージを読むことができます。

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="例は、bot の事前メッセージを見ているユーザーを示しています。" border="false":::

### <a name="use-tabs-with-bots"></a>Bot でタブを使用する

タブを使用すると、ボットを使いやすくすることができます。 たとえば、ボットで作業項目を作成できる場合は、すべてのアイテムを1つのタブ内の中央の場所に表示することをお勧めします。 [タブのデザイン](../../tabs/design/tabs.md)に関する詳細を参照してください。

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="例は、タブを使用して bot コンテンツを整理する方法を示しています。" border="false":::

## <a name="manage-a-bot"></a>Bot を管理する

ユーザーは bot の設定を変更できる必要があります。 この機能は bot コマンドで提供できますが、通常は、すべての設定を [タスクモジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) に含めることをお勧めします (次の例を参照)。

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="例は、bot の設定を構成するためのタスクモジュールを示しています。" border="false":::

## <a name="best-practices"></a>ベスト プラクティス

### <a name="content"></a>コンテンツ

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-establish-a-clear-persona"></a>Do: 明快なペルソナを設定する

Bot の雰囲気をよく理解しているかどうか、「ファクトのみ」、またはスーパー quirky? さまざまなシナリオでどのように対応する必要があるか。 Bot のペルソナを計画および文書化することで、自然で凝集しているように見える応答を簡単に記述できるようになります。

詳細については、「 <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft TEAMS UI Kit (Figma)</a> 」を参照してください。

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a>Do: bot が実行できることを明確に伝える

ウェルカムメッセージとツアーは、ユーザーが bot に対して何ができるかを理解するのに役立ちます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="dont-obscure-your-bots-features"></a>しない: bot の機能を不明瞭にする

最初のインプレッションの問題。 Nondescript サインインメッセージが表示された場合、ユーザーが混乱したり疑わしいことがあります。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-recognize-non-questions"></a>Do: 質問以外の項目を認識する

Bot は、よくあるスペルミスと口語を考慮しながら、"Hi"、"Help"、"ありがとうございます" などのメッセージに応答できるようにする必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a>成功へのチャンスを見逃さないようにします。

ユーザーによっては、実際の人物のような会話を自然に流すことが予想されます。 単純なメッセージへの clumsy 応答を避けるようにしてください。

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a>トラブルシューティング

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-provide-help"></a>Do: ヘルプを提供する

Bot が要求を満たすことができない場合は、ユーザーが bot との対話について自分で教育する方法を提供します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="dont-leave-users-stranded"></a>いいえ: ユーザーを残されたままにします

問題のトラブルシューティングができない場合、ユーザーは bot をすぐに放棄します。

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a>複雑な相互作用

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-use-task-modules-or-tabs"></a>Do: タスクモジュールまたはタブを使用する

Bot が応答を提供し、さらにいくつかの手順が必要な場合は、タスクモジュールまたはタブにリンクして、タスクまたはフローを完了できます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a>いいえ: 複数ターンの対話を面倒にする

1つのタスクを完了するための広範な会話は、遅く、過度に複雑です。 また、開発者は、状態の変更 (会話のタイムアウト、"キャンセル" メッセージの送信など) を考慮する必要があります。

   :::column-end:::
:::row-end:::

### <a name="privacy"></a>プライバシー

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a>Do: 個人のコンテキストに機密情報のみを表示する

Bot がグループチャットまたはチャネルにある場合は、機密情報を表示するためにユーザーをプライベートな場所 (タスクモジュール、タブ、ブラウザーなど) に送ることをお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="この例では、ボットのベストプラクティスを示しています。" border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a>いいえ: 一部のコンテンツは、すべてのユーザーに表示されることを意図したものではありません

Bot は、ユーザーのグループに機密情報を公開することはできません。

   :::column-end:::
:::row-end:::

## <a name="learn-more"></a>詳細情報

このような他のガイドラインは、ボット設計に役立てることができます。

* [個人用アプリを設計する](../../concepts/design/personal-apps.md)
* [アダプティブカードの設計](../../task-modules-and-cards/cards/design-effective-cards.md)
* [タスクモジュールを設計する](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="validate-your-design"></a>設計を検証する

アプリを AppSource に発行することを計画している場合は、一般的にアプリが送信中に失敗する原因となる設計上の問題について理解しておく必要があります。

> [!div class="nextstepaction"]
> [設計検証ガイドラインの確認](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
