---
title: ボットの設計ガイドライン
description: Bot を作成するためのガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスフレームワークの bot トーク
ms.openlocfilehash: f59a1e9c280f27567692b4d10341db79d05c3464
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675040"
---
# <a name="start-talking-with-bots"></a>Bot との会話を開始する

Bot は、特定のタスクセットを実行する会話アプリです。 これにより、ユーザーとのコミュニケーションが可能になり、質問に回答して、変更について事前に通知する機会が得られます。 これらは、お客に到達するための最適な方法です。

---

## <a name="guidelines"></a>ガイドライン

### <a name="avatars"></a>アバター

Teams のボットアバターは、六角形のようになっているため、ユーザーはユーザーではなく bot に話しかけていることがすぐにわかります。 アバターを正方形として送信し、自分でトリミングします。 アバターに関しては、2フィート離れて高いコントラストを使用することをお勧めします。

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a>ボタン

カードごとに最大6つのボタンをサポートしています。 ボタンテキストを記述する場合は簡潔にする必要があります。ほとんどのボタンは、自分のタスクにのみ対処する必要があることに注意してください。

### <a name="graphics"></a>グラフィックス

グラフィックスはストーリーを伝えるのに適した方法ですが、すべての bot がグラフィックスを必要とするわけではないため、これらを使用して最大の影響を受けることができます。

### <a name="responding-to-users-and-failing-gracefully"></a>ユーザーに応答して、正常にエラーを発生させる

Bot は、一般的なスペルミスと口語を考慮しながら、' Hi '、' Help '、' どうも ' などに応答することもできます。 例:

#### <a name="x2713-hello"></a>&#x2713; Hello

`Hi` `how are you` `howdy`

#### <a name="x2713-help"></a>&#x2713; のヘルプ

`What do you do?` `How does this work?` `What the heck?`

#### <a name="x2713-thanks"></a>&#x2713; よろしくお願いいたします。

`Thank you` `thankyou` `thx`

Bot は、次の種類のクエリと入力を処理できる必要があります。

* **認識**される質問: これらは、ユーザーから予想される "ベストケースのシナリオ" 質問です。
* **認識されない問題**: サポートされていない機能、ランダムな情報、またはユーザーが bot で curse を希望する場合についてのクエリ。
* **認識されない質問**: 判読不能な入力 (つまり、不自然)。

Bot のパーソナリティと応答の種類の例:

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> Bot スクリプトを記述するときは、「応答が画面にキャプチャおよび共有されている場合は会社の embarrassed になりますか?」という質問をします。

### <a name="understanding-what-users-are-trying-to-say"></a>ユーザーが発言しようとしていることを理解する

#### <a name="use-a-thesaurus-for-synonyms"></a>類義語辞典を使用する

バリエーションを使用している場合は、シソーラスを使用して、各クエリのさまざまな解釈を生成するのに役立つように、できるだけ多くの背景からユーザーを取得します。

#### <a name="make-use-of-telemetry-and-interviews"></a>テレメトリとインタビューを利用する

ユーザーが何を言っているか、ボットを照会する際にどのような意図があるかを確認します。 これは、さまざまな場所や企業の種類でユーザーを取得するときに、継続的なプロセスになります。 言語を使用した言語認識と意図的なマッピングを微調整することができます ([LUIS](/azure/cognitive-services/luis/what-is-luis))。

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a>ボットを使用してユーザーに連絡する頻度を指定します。

#### <a name="x2713-when-a-state-has-changed"></a>状態が変更されたときの &#x2713;

たとえば、割り当てが完了としてマークされている場合、バグが変更された場合、新しいソーシャルメディアが利用可能になった場合、またはポーリングが完了した場合などです。

#### <a name="x2713-when-the-timing-is-right"></a>タイミングが正しい場合の &#x2713;

Bot は、特定の頻度でユーザーまたはチャネルに通知を送信して、デイリーダイジェストのように機能することができます。

ユーザーをコントロールのままにします。 頻度と優先度を含む通知設定を提供します。

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a>タブの使用

タブを使用すると、ボットの機能が向上します。 タブでは、次のものを作成できます。

### <a name="x2713-a-place-to-host-standing-queries"></a>サバイバルクエリをホストする場所を &#x2713;

Bot と1人のユーザーの個人的な会話では、タブでユーザー固有の情報やリストを格納できます。 また、よく寄せられる質問 (Faq) に対してボットへの回答を維持するための適切な場所でもあります。そのため、ユーザーがたずねる必要はありません。

### <a name="x2713-a-place-to-finish-a-conversation"></a>会話を終了するための場所の &#x2713;

カードからタブにリンクすることができます。 Bot が応答を提供し、さらにいくつかの手順が必要な場合は、タブにリンクしてタスクまたはフローを完了できます。

### <a name="x2713-a-place-to-provide-some-help"></a>いくつかのヘルプを提供する場所を &#x2713;

Bot との通信方法をユーザーに伝えるタブを追加します。 何らかの状況や Faq を提供することができます。

![ヘルプの提供](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> サイトのパーツをタブに埋め込むと、ユーザーがサービスを使用するときに会話のコンテキストを維持するのに役立ちます。 ブラウザーでサービスを起動して、アプリ間で切り替えを行う必要がなくなります。

---

## <a name="best-practices"></a>ベスト プラクティス

### <a name="x2713-bots-arent-assistants"></a>&#x2713; Bot がアシスタントでない

Cortana や bot などのエージェントとは異なり、スペシャリストとして機能します。

### <a name="x2713-discourage-chitchat"></a>&#x2713; 防ぐ chitchat

Bot が会話用に構築されていない場合は、chitchat をタスク完了にリダイレクトする方法を検索します。

### <a name="x2713-introduce-some-personality"></a>&#x2713; を紹介します。

お客様の bot の個性を製品の声と同じにしておきます。 お客様の企業の bot と考えてください。

### <a name="x2713-maintain-tone"></a>トーンを維持 &#x2713;

トーンがわかりやすく、明るいかどうかを判断するために、"ファクトのみ"、または super quirky を使用します。

### <a name="x2713-encourage-easy-task-flow"></a>簡単なタスクフローを促す &#x2713;

完全な形式の質問を引き続き許可しながら、複数ターンの対話をサポートします。 次の手順を予測することで、ユーザーはタスクフローをより簡単に理解できるようになります。

ユーザーがタスクを完了するためにいくつかの手順を実行する場合は、各手順を通じて bot に対して実行を許可し、より迅速なパスを提案することによって終了します。 たとえば、ユーザーがいくつかの会話を行って会議を設定した場合 (最初に会議を指定し、次にその人物との識別を行い、時刻を指定して、その日を示す場合)、次の提案に従って会話を終了します。「1:00 明日で Bob を使用して会議をスケジュールすることができます。