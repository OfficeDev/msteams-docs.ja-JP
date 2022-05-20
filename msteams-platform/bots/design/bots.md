---
title: ボットをデザインする
description: Teams のボットをデザインして、Microsoft Teams UI Kit を取得するする方法をご紹介します。
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: 67f67535994bde9871cdaa7be8081e05ccbf1a1d
ms.sourcegitcommit: aa95313cdab4fbf0a9f62a047ebbe6a5f1fbbf5d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2022
ms.locfileid: "65602300"
---
# <a name="designing-your-microsoft-teams-bot"></a>Microsoft Teams のボットをデザインする

ボットは、特定のタスクを実行する会話型アプリです。 <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a> をベースに、ボットはユーザーと通信し、ユーザーの質問に答え、変更などのイベントをプロアクティブに通知します。 ボットは、連絡を取るのに最適な方法です。

> [!IMPORTANT]
> ボットは Government Community Cloud (GCC) 環境とGCC High環境では使用できますが、米国国防総省 (DOD) 環境では使用できません。

アプリのデザインに役立てるために、次の情報では、Teams でユーザーがどのようにボットを追加、使用、管理できるかを説明、図解しています。

## <a name="microsoft-teams-ui-kit"></a>Microsoft Teams UI Kit

Microsoft Teams UI Kit には、必要に応じて変更できる要素を含む、より包括的なボット デザインのガイドラインが掲載されています。

> [!div class="nextstepaction"]
> [Microsoft Teams UI Kit (Figma) を入手する](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a>ボットの追加

ボットは、チャット、チャネル、個人用アプリで利用できます。

### <a name="mobile"></a>モバイル

ユーザーは、@メンションを使用してデスクトップに追加されたボットにアクセスできます。

:::image type="content" source="../../assets/images/bots/mobile-access-bot-chat-at-mention.png" alt-text="例では、@メンションを使用してグループ チャットのモバイル ボットにアクセスする方法をご紹介します。" border="false":::

### <a name="desktop"></a>Desktop

ユーザーは、次の方法のいずれかでボットを追加できます。

* Teams ストアから。
* Teams の左側にある **[詳細]** アイコンを選択してアプリのフライアウトを使用する。
* 新規チャットや作成ボックスに@メンションを使用する (次の例ではグループ チャットでのやり方を示しています)。

    :::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="例では、@メンションを使用してグループ チャットにボットを追加する方法をご紹介します。" border="false":::

## <a name="introduce-a-bot"></a>ボットの導入

ボットが自己紹介し、何ができるのかを説明することが重要です。 この最初のやり取りによって、ユーザーはボットで何ができるかを理解し、その制限事項を知り、そして最も重要なことは、ボットとの対話を快適に行うことができます。

### <a name="welcome-message-in-a-one-on-one-chat"></a>1 対 1 のチャットでのウェルカム メッセージ

個人的なコンテキストでは、ウェルカム メッセージはボットのトーンを決めるものです。 メッセージには、挨拶、ボットができること、対話方法の提案が含まれます。 たとえば、「... について聞いてみてください」などです。 可能であれば、これらの提案は、サインインしなくても保存された応答を返す必要があります。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/bots/mobile-bot-personal-welcome.png" alt-text="モバイルの個人アプリでのボット導入例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="個人アプリでのボット導入例を示します。" border="false":::

### <a name="welcome-message-in-channels-and-group-chats"></a>チャネルやグループ チャットでのウェルカム メッセージ

チャネルやグループ チャットでのボットの紹介は、個人用スペース (個人用アプリなど) とは多少異なる必要があります。 実生活では、大勢の人がいる部屋に入った場合に、既にいる人を歓迎するのではなく、自己紹介をするはずです。 その考え方は、ボットのデザインにも生かされています。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/bots/mobile-bot-group-welcome.png" alt-text="モバイルの共同作業コンテキストでのボット導入例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="共同作業コンテキストでのボット導入例を示します。" border="false":::

### <a name="bot-authentication-with-single-sign-on"></a>シングル サインオンを使用したボット認証

ユーザーがボットにメッセージを送る場合、そのボットのすべての機能を利用するにはサインインが必要な場合があります。 シングル サインオン (SSO) を使用することで認証プロセスを簡略化できます。

忘れてはいけないのが、ボットのコマンド メニュー (**可能な対処**) では、サインアウトするためのコマンドも用意する必要があります。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/bots/mobile-bot-sso-example.png" alt-text="モバイルでサインイン ボタンのあるボットの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="サインイン ボタンのあるボットの例を示します。" border="false":::

### <a name="tours"></a>ツアー

ウェルカム メッセージや "ヘルプ "コマンドのようなものにボットが応答する場合にツアーを含めることができます。 ボットにできることを説明するには、ツアーが最も効果的です。 必要に応じて、アプリのその他の機能を説明するのにも最適です。 たとえば、メッセージ拡張機能のスクリーンショットなどです。

> [!IMPORTANT]
> ログインしなくてもツアーに参加できることが必要です。

### <a name="one-on-one-chats"></a>1 対 1 のチャット

個人用アプリでは、カルーセルでボットやお使いのアプリのその他の機能の概要を効果的に伝えることができます。 ユーザーがボットのコマンドを試すことができるボタンを含めることが推奨されます。 たとえば、「**タスクを作成する**」などです。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-personal.png" alt-text="モバイルの 1 対 1 のチャットでのボット ツアーの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="1 対 1 のチャットでのボット ツアーの例を示します。" border="false":::

### <a name="channels-and-group-chats"></a>チャネルとグループ チャット

チャネルやグループ チャットでは、ツアーはモーダル ([タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)とも呼ばれます) で開き、現在進行中の会話に干渉しないようにします。 また、ツアーにロール ベースのビューを実装することも可能です。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/bots/mobile-bot-tour-channel.png" alt-text="モバイルのチャネルでのボット ツアーの例を示します。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="チャネルでのボット ツアーの例を示します。" border="false":::

## <a name="chat-with-a-bot"></a>ボットとチャットする

ボットは、Teams のメッセージング フレームワークに直接統合されます。 ユーザーはボットとチャットして質問に回答してもらったり、コマンドを入力して特定のタスクを実行してもらったりすることができます。 ボットは、お使いのアプリへのチャットを介してユーザーに変更や更新をプロアクティブに通知することができます。

### <a name="chat-with-a-bot-in-different-contexts"></a>さまざまなコンテキストでボットを使用したチャット

ボットは次のような場面で使用できます。

* **個人用アプリ**: 個人用アプリでは、ボットには専用のチャット タブがあります。
* **1 対 1 のチャット**: ユーザーがボットとプライベートな会話を開始することができます。 個人用アプリでボットを使うのと同様のエクスペリエンスです。
* **グループ チャット**: グループ チャットでは、ボットを @メンションすることで、ボットと対話することができます。
* **チャネル**: ユーザーは、チャネルでボットと対話することができます。 作成ボックスでボット名を　@メンションします。 このコンテキストでは、ボットはチャネルだけでなく、チーム全体で使用できることを忘れないでください。

### <a name="anatomy"></a>構造

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/bots/mobile-bot-anatomy.png" alt-text="モバイル ボットの構造的な例を示します。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリ名とアイコン**|
|2|**[チャット] タブ**: ボットと会話するための空間を開きます (個人用アプリのみ該当)。|
|3|**[カスタム] タブ**: アプリに関連するその他のコンテンツを開きます。|
|4|**チャット バブル**: ボットの会話は、Teams のメッセージング フレームワークを使用しています。|
|5|**アダプティブ カード**: ボットの応答にアダプティブ カードが含まれる場合、カードはチャット バブルの幅いっぱいに表示されます。|

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="ボットの構造的な例を示します。" border="false":::

|カウンター|説明|
|----------|-----------|
|1|**アプリ名とアイコン**|
|2|**[チャット] タブ**: ボットと会話するための空間を開きます (個人用アプリのみ該当)。|
|3|**[カスタム] タブ**: アプリに関連するその他のコンテンツを開きます。|
|4|**[バージョン情報] タブ**: アプリの基本情報を表示します。|
|5|**チャット バブル**: ボットの会話は、Teams のメッセージング フレームワークを使用しています。|
|6 |**アダプティブ カード**: ボットの応答にアダプティブ カードが含まれる場合、カードはチャット バブルの幅いっぱいに表示されます。|
|7 |**コマンド メニュー**: ボットの標準コマンド (ユーザーによる定義) を表示します。|

### <a name="command-menu"></a>コマンド メニュー

コマンド メニューには、ボットが常に応答するようにする単語や語句のリストが用意されています。 ボットと会話しているときに、作成ボックスの上にコマンド メニューが表示されます。 コマンドを選択した場合に、そのコマンドがメッセージに挿入されます。

コマンドのリストは簡潔である必要があります。 メニューは、ボットの主要な機能を強調するためだけのものです。 また、コマンドも簡潔に保持します。 例えば、**手伝ってもらえますか?** の代わりに **ヘルプ** というコマンドを作成します。

会話の状態に関係なく、コマンド メニューは常に使用可能である必要があります。

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="ボットのコマンド メニューの例を示します。" border="false":::

## <a name="understand-what-people-are-saying"></a>ユーザーの話を理解する

シソーラスを使ったり、できるだけ多くの異なるバックグラウンドを持つユーザーの協力を得て、標準的な質問に対するさまざまな解釈を生成します。

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="ボットが ‘こんにちは’ を解釈する方法を示す図。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="ボットが ‘ヘルプ’ を解釈する方法を示す図。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="ボットが ‘ありがとう’ を解釈する方法を示す図。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a>メッセージから意図やデータを抽出

メッセージやクエリに応じて、相手がボットに何を求めているかをキャプチャする、意図の認識を目指してボットをデザインします。 意図は、メッセージやクエリを、アクションの影響を受ける 1 つ以上のデータ オブジェクトのある単一のアクションとして分類します。 

次の例は、ボットに送信されるメッセージに含まれるユーザーの意図とデータの概要です。

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="‘シアトル行きの航空券を予約する’ という文の場合、ユーザーの意図は ‘航空券の予約’ であり、データは ‘シアトル’ であることを示す例。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="‘何時に店が開くか’ という文の場合、ユーザーの意図は ‘何時’ であり、データは ‘開く’ です。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="‘配送のボブと午後 1 時に会議をスケジュールする’ という文の場合、ユーザーの意図は ‘会議のスケジュール’ であり、データは ‘午後 1 時’ と ‘配送のボブ’ です。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a>分析と機能強化

ボットとのチャットでのユーザーの発言をご紹介します。 これは、さまざまな場所や組織でユーザーが増えていく中で、継続的で反復的な手順です。 Microsoft Language Understanding (LUIS) を使用して、ボットの言語認識や意図のマッピングを調節することができます。

* [LUIS を理解する](/azure/cognitive-services/luis/artificial-intelligence): LUIS が AI を使用してアプリのデータに自然言語理解 (NLU) を提供する方法をご紹介します。
* [LUIS との統合](https://www.luis.ai/): 機械学習モデルを作成する複雑な手順を通すことなく、ボットに自然言語機能を追加します。

## <a name="use-cases"></a>使用例

### <a name="simple-queries"></a>単純なクエリ

ボットは、クエリと完全に一致する内容や関連して一致するグループを配信して、曖昧さを解消することができます。 関連する一致については、リスト カードを使用してコンテンツをグループ化します。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/bots/mobile-bot-simple-query.png" alt-text="モバイルでのボットとの単純なクエリの対話を示す例。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="ボットとの単純なクエリの対話を示す例。" border="false":::

### <a name="multi-turn-interactions"></a>複数回の対話

ボットは、完全な要求や質問をサポートすることができますが、複数回の対話を処理することもできる必要があります。 次の手順の可能性を予測することで、ユーザーは (包括的な要求を作成することを想定するのではなく) 完全なタスク フローをより簡単に作成できます。

次の例では、ボットはそれぞれのメッセージに対して、次にしたいことのオプションを応答します。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/bots/mobile-bot-multi-turn.png" alt-text="モバイルでのボットとの複数回の対話を示す例。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="ボットとの複数回の対話を示す例。" border="false":::

### <a name="reach-out-to-users"></a>ユーザーへの働きかけ

プロアクティブなメッセージングでは、ボットは個人、グループ チャット、またはチャネルに関連する通知を特定の頻度で送信するダイジェストのように機能します。 ボットは、ドキュメントに何か変更があった場合や、作業項目を閉じた場合に、メッセージを送信することができます。

#### <a name="mobile"></a>モバイル

ユーザーが、ボットが別のチャネルでメッセージを送ってきたことをについて通知を受け取る例を次に示します。

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message-toast.png" alt-text="モバイルでボットが他のチャネルからユーザーにプロアクティブにメッセージを送るトーストを示す例。" border="false":::

そのチャネルでは、ユーザーはボットからのメッセージを読むことができます。

:::image type="content" source="../../assets/images/bots/mobile-bot-proactive-message.png" alt-text="モバイルでユーザーがボットのプロアクティブなメッセージを見ている様子を示す例。" border="false":::

#### <a name="desktop"></a>Desktop

ユーザーが、ボットが別のチャネルでメッセージを送ってきたことをトースト通知で受け取る例を次に示します。

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="ボットが他のチャネルからユーザーにプロアクティブにメッセージを送るトーストを示す例。" border="false":::

そのチャネルでは、ユーザーはボットからのメッセージを読むことができます。

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="ユーザーがボットのプロアクティブなメッセージを見ている様子を示す例。" border="false":::

### <a name="use-tabs-with-bots"></a>ボットでタブを使用する

個人用アプリでは、タブはボットが実行可能な機能を補完できます。 たとえば、ボットが作業項目を作成できる場合、それらのアイテムをタブ内の中心的な場所に表示できると便利です。詳細については、[タブのデザイン](../../tabs/design/tabs.md) を参照してください。

#### <a name="mobile"></a>モバイル

:::image type="content" source="../../assets/images/bots/mobile-bot-with-tab.png" alt-text="モバイルでタブを使用してボットのコンテンツを整理する方法を示す例。" border="false":::

#### <a name="desktop"></a>Desktop

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="タブを使用してボットのコンテンツを整理する方法を示す例。" border="false":::

## <a name="manage-a-bot"></a>ボットの管理

ユーザーがボットの設定を変更できるようにします。この機能をボット コマンドで提供することもできますが、通常は [タスク モジュール](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) にすべての設定を含める方が効率的です (次に例を示します)。

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="ボットの設定を構成するタスク モジュールを示す例。" border="false":::

## <a name="best-practices"></a>ベスト プラクティス

これらの推奨事項を使用して、高品質のアプリ エクスペリエンスを作成します。

### <a name="content"></a>Content

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="明確なペルソナを設定するためのボットのベスト プラクティスを示す例。" border="false":::

#### <a name="do-establish-a-clear-persona"></a>するべきこと: 明確なペルソナの設定

お使いのボットのトーンは、親しみやすく軽快なものか、”事実だけを伝える” ものか、それとも超気まぐれか。 さまざまなシナリオでどのように対応すべきか。 ボットのペルソナを計画して文書化することで、自然でまとまりのある応答を簡単に記述することができます。

ボット向けの記述の詳細については、「<a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma)</a>」参照してください。

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="ボットにできることを明確に伝達することを示す例。" border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a>するべきこと: ボットにできることを明確に伝達する

ウェルカム メッセージやツアーでは、お使いのボットでできることを理解してもらいます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="ボットの機能をぼかさないことを示す例。" border="false":::

#### <a name="dont-obscure-your-bots-features"></a>してはいけないこと: ボットの機能をぼかす

第一印象が大切です。何の変哲もないサインイン メッセージが表示されると、ユーザーは混乱したり疑ったりするでしょう。

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="ボットはノンクエスチョンを認識する必要があることを示す例。" border="false":::

#### <a name="do-recognize-non-questions"></a>するべきこと: ノンクエスチョンを認識する

ボットは、"やあ"、"ヘルプ"、"ありがとう" などのメッセージに対応し、一般的なスペルミスや口語表現にも対応できる必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="シンプルなボット メッセージに対する不自然な応答を回避する必要があることを示す例。" border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a>してはいけないこと: 喜ぶチャンスを逃す

ユーザーの中には、実際の人間との会話のような自然な流れを期待する人もいます。 シンプルなメッセージには無難な返答を心がけましょう。

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a>トラブルシューティング

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="ボットは、ユーザーがボットの使用方法を理解するためサポートを行う必要があることを示す例。" border="false":::

#### <a name="do-provide-help"></a>するべきこと: ヘルプを用意する

ボットが要求を満たせない場合は、ボットとの対話についてボット自身を教育するための方法をユーザーが用意します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="ボットがユーザーを立ち往生させてはいけないことを示す例。" border="false":::

#### <a name="dont-leave-users-stranded"></a>してはいけないこと: ユーザーを立ち往生させる

問題を解決できなければ、ユーザーはすぐにボットを放棄してしまいます。

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a>複雑な相互作用

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="ボットで複雑な対話をするためにタスク モジュールやタブを使用できることを示す例。" border="false":::

#### <a name="do-use-task-modules-or-tabs"></a>するべきこと: タスク モジュールやタブの使用

ボットが答えを出しても、さらにいくつかの手順が必要な場合は、タスク モジュールやタブにリンクして、タスクやフローを完成させることができます。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="ボットでは複数回の対話を回避する必要があることを示す例。" border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a>してはいけないこと: 複数回の対話を面倒にする

単一のタスクを完了するのに膨大な量の会話をするのは時間がかかり、複雑すぎます。 また、開発者は、状態の変化 (会話がタイムアウトしたり、”キャンセル” メッセージを送信するなど) を考慮する必要があります。

   :::column-end:::
:::row-end:::

### <a name="privacy"></a>プライバシー

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="ボットは個人的なコンテキストで個人情報のみを表示する必要があることを示す例。" border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a>するべきこと: 機密情報を個人的なコンテキストでのみ表示する

ボットがグループ チャットやチャネル内にある場合は、機密情報を閲覧するために、ユーザーをプライベートな場所 (タスク モジュール、タブ、ブラウザなど) に誘導することをお勧めします。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="ボットがグループやユーザーに機密情報を公開してはいけないことを示す例。" border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a>してはいけないこと: すべてのユーザーが閲覧できないコンテンツがある

お使いのボットでは、機密情報をグループに公開してはいけません。

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>関連項目

以下のガイドラインは、ボット デザインに役立つ可能性があります。

* [個人用アプリをデザインする](../../concepts/design/personal-apps.md)
* [アダプティブ カードをデザインする](../../task-modules-and-cards/cards/design-effective-cards.md)
* [タスク モジュールをデザインする](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
