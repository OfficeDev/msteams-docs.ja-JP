---
title: Microsoft Teams アプリテンプレート
description: Microsoft Teams プラットフォームのアプリテンプレートのリンクと説明
keywords: Microsoft Teams テンプレートサンプルのデモ
ms.openlocfilehash: 7bbd1093a7d3d2ed29498ce79051549621784b57
ms.sourcegitcommit: a955121927090ee01173d70628c388991f53d23b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2020
ms.locfileid: "42416853"
---
# <a name="app-templates-for-microsoft-teams"></a>Microsoft Teams のアプリテンプレート

アプリテンプレートとは、コミュニティ主導で、オープンソースで、GitHub 上で利用可能な Microsoft Teams 用のプロダクション対応アプリのことです。 それぞれに、組織のためにアプリを展開してインストールするための詳細な手順が記載されており、すぐにインストールして使用を開始できるアプリを用意しています。 完全なソースコードも利用できます。そのため、詳細について確認したり、コードをフォークして、特定のニーズを満たすように変更したりすることができます。

## <a name="key-benefits-of-using-app-templates"></a>アプリテンプレートを使用する主な利点

* **プラグアンドプレイの操作:** すべてのアプリテンプレートには、Microsoft Azure で必要なすべてのサービスをホストできる展開スクリプトが含まれています。 アプリを展開するためのコーディングは必要ありません。
* **運用可能なコード:** アプリテンプレートは、セキュリティとインフラストラクチャの推奨されるベストプラクティスに準拠しており、それらに加えられたすべてのコミュニティの変更をレビューして、引き続き準拠していることを確認します。
* **カスタマイズと拡張:** すべてのアプリテンプレートを展開する準備ができましたが、コードベースと展開スクリプト全体が提供されるので、独自のニーズに合わせてカスタマイズまたは拡張することが容易になります。
* **サポート & 詳細なドキュメント:** すべてのアプリテンプレートには、ソリューションのアーキテクチャ、展開、および構成手順に関するエンドツーエンドのドキュメントが付属しています。 リポジトリも監視されるので、GitHub で問題を発生させることで、発生した問題を報告してください。

## <a name="celebrations"></a>お祝い

[記念] は Teams アプリであり、チームメンバーは、他の誕生日、記念日、その他の定期的なイベントを担当することができます。 すべてのチームメンバーの特別な状況を記録して、イベントの作成時に選択されたすべてのチームでフレンドリメッセージを送信し、チームメンバーが自分の一日に特別な印象を感じられるようにします。

アプリは、すべてのチームメンバーが自分のイベントを個人的に追加および表示し、ユーザーがイベントを共有するチームを選択できるようにするための簡単なインターフェイスを提供します。

[GitHub で取得する](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="company-communicator"></a>社内コミュニケーター

会社の Communicator アプリを使用すると、企業チームはチャットを介して複数のチームまたは多数の従業員宛てのメッセージを作成して送信することができます。 このテンプレートを、新しいイニシアチブのアナウンス、従業員のオンボード、モダンラーニング、開発、組織全体のブロードキャストなど、複数のシナリオで利用できます。

アプリは、指定されたユーザーがメッセージを作成、プレビュー、共同作業、および送信するための簡単なインターフェイスを提供します。

これにより、メッセージを確認したり操作したりしたユーザー数について、カスタムテレメトリなどのカスタムの対象化通信機能を構築するための基盤が提供されます。

[GitHub で取得する](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![FAQ + gif](../assets/images/CompanyCommunicatorCompose.png)

## <a name="faq-plus"></a>FAQ プラス

話し言葉 Q&ボットは、ユーザーからよく寄せられる質問に対する回答を簡単に提供する方法です。 ただし、bot が失敗したときにループに人間が存在しないため、ほとんどのボットはユーザーとの通信に失敗することがあります。 FAQ bot は、問題が解決できないときにループを処理する bot&ボットです。 この場合は、bot がサポート技術情報に含まれている場合、ボットに質問をして応答を求めることができます。 できない場合は、ユーザーはクエリを送信して、チーム内から通知を受け取ることによってサポートを提供できる専門家の事前に構成されたチームに投稿することができます。

[GitHub で取得する](https://github.com/OfficeDev/microsoft-teams-faqplusplus-app)

> [!NOTE]
> FAQ に加えて、**バージョン 2**の2020リリースでは、専門家のチームが次のことを実行できるようにすることで、改善された Q&サポートしています。
>
> &#x2714; メッセージ拡張機能を使用して、新しい Q&をナレッジベースに直接追加します。
>
> &#x2714; を編集および削除するには、bot によって追加されたペア&Q を追加します。
>
> &#x2714; Q&のリビジョン履歴を追跡します。
>
> &#x2714;[アダプティブカード](/task-modules-and-cards/cards/cards-reference#adaptive-card)として表示するには、追加の詳細を含む回答を構成します。
>
>[**GitHub で取得する**](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)
>
>

![FAQ + gif](../assets/images/FAQPlusEndUser.gif)

## <a name="hr-support"></a>HR サポート

HR サポート bot は、問題が解決できないときに、そのループの人事チームのサポートプロフェッショナル/専門家を支援する bot&のフレンドリな質問です。 この場合は、bot がサポート技術情報に含まれている場合、ボットに質問をして応答を求めることができます。 できない場合は、ユーザーはクエリを送信して、チーム内から通知を受け取ることによってサポートを提供できる専門家の事前に構成されたチームに投稿することができます。 また、bot は、質問で事前に構成されたタグを検索することにより、推奨される人事ポリシー/質問へのリンクを提案します。 これらのタイルは、クイックリファレンスとして、関連付けられたタブにもあります。 人事サポートは、軽いウエイト QnA に適しており、組織内で新しいプロジェクト/イニシアチブを開始する際の迅速なサポートを提供します。

[GitHub で取得する](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![HR サポート](../assets/images/expert-user.png)

## <a name="list-search"></a>リスト検索

Microsoft Teams でのコラボレーションは、多くの場合、SharePoint リスト内のアイテムに含まれている情報を参照します。 目的のアイテムへのリンクを貼り付けるだけで、すべてのユーザーに対して、会話からのコンテキストの切り替え、必要な情報の検索、および会話を続行するために Teams に戻ることが強制されます。 会話は、通常、新しいコメントを確認し、アイテム内に含まれる情報を更新するために、参照アイテムに再び切り替える必要があります。 このコンテキストの切り替えは、グループ作業をスムーズにするための障壁を作成し、その亀裂についてのレシピとなります。

このような問題を軽減するために、リスト検索アプリテンプレートに移動することになります。 数百万人のユーザーが SharePoint を使用して、組織内のコアワークフローの一部を強化します。 ただし、リストに関する共同作業は、特に面倒な場合があります。 Microsoft Teams でリスト検索アプリテンプレートを使用すると、ユーザーは SharePoint リストアイテムの情報をチャット会話内に直接挿入して、リンクをチャットに挿入するだけで済むようになったため、コンテキスト切り替えが軽減されます。 この情報は、簡単に読める自動フォーマットのカードとして挿入され、ユーザーが会話に参加し続けるのを支援します。

[GitHub で取得する](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![検索アプリを一覧表示する](../assets/images/list-search-template.png)

## <a name="custom-stickers"></a>カスタム ステッカー

自己表現は、正常なチームのカルチャにとって中心的なものです。 このアプリテンプレートは、ユーザーが Microsoft Teams 内でカスタムステッカーと Gif を使用できるようにする[メッセージング拡張機能](~/messaging-extensions/what-are-messaging-extensions.md)です。 このテンプレートを使用すると、web ベースの構成を簡単に行うことができます。これにより、エンドユーザーが使用する Gif/ステッカー/画像を構成アクセス権を持つすべてのユーザーがアップロードできるようになります。

このアプリでは、ストレージと共有のメカニズムとして、SharePoint サイトや個々のチャネルへのアクセスを必要とせずに、teams 間で画像、Gif、ステッカーを簡単に共有することもできます。 たとえば、製品チームは、プログラムを使用して、製品の画像や Gif をソーシャルメディア、マーケティング、営業チームに簡単に共有できます。 新しい画像/Gif が利用可能になったときに、特定の teams/個人に通知フローをトリガーすることによって、このアプリを拡張することもできます。

[GitHub で取得する](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![ステッカーアプリ](../assets/images/stickers.png)

## <a name="icebreaker"></a>アイスブレーカー

Icebreaker は[Microsoft Teams の bot](../bots/what-are-bots.md)で、チームは、2つのランダムなチームメンバーを毎週1つずつペアにすることによって近づくことができます。 Bot は、両方のメンバーに対して動作する空き時間を自動的に提案することで、スケジュールを簡単にします。 パーソナル接続を強化し、このアプリを使用して緊密な knit コミュニティを構築します。

Icebreaker アプリは、チーム全体にわたる個人の接続を促進するだけでなく、組織内の利息ベースコミュニティを cultivate するのに役立ちます。 たとえば、このアプリを DevOps の趣味グループに対して使用すると、アイデアやベストプラクティスつれを組織全体に分散させることができます。

[GitHub で取得する](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Icebreaker アプリ](../assets/images/icebreaker.png)

## <a name="scrum-status-bot"></a>スクラム状態 bot

スクラム状態 bot は、ユーザーが非同期のスタンドアップ会議を実行し、ユーザーが毎日の更新を共有するための簡単な方法を提供できる、シンプルなスクラムアシスタントの bot です。 Teams グループチャットで機能するように設計されており、すべてのメンバーがスクラムに貢献できます。 1つはスクラムを開始および終了し、実行中のスクラムで他者が行った更新を表示することができます。

[GitHub での Git it](https://github.com/OfficeDev/microsoft-teams-app-scrumstatus)

![スクラム状態 Bot](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="crowdsourcer-bot"></a>Crowdsourcer bot

Crowdsourcer は、チームが照会した情報をグループメンバーから共同で提供する[Microsoft teams bot](../bots/what-are-bots.md)です。 これは、よく寄せられる質問に回答するための最適な方法であり、参加者が積極的に協力して、楽しくて役に立つ情報リソースに投稿することを可能にします。

[Github で取得する](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Crowdsource エンドユーザーの操作](../assets/images/crowdsourcer.png)

## <a name="expert-finder-bot"></a>エキスパートファインダー

専門家の Finder は、スキル、関心事、教育の属性に基づいて特定の組織のメンバーを識別する[Microsoft Teams の bot](../bots/what-are-bots.md)です。 メンバーは、Azure Active Directory ユーザープロファイルのキーワード検索に一致する組織内の専門家を検索します。

[GitHub で取得する](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![エキスパートファインダー検索結果のデモ](../assets/images/expert-finder.png)

## <a name="book-a-room-bot"></a>書籍-a-room bot

書籍-a room は[Microsoft Teams の bot](../bots/what-are-bots.md)で、現在の時刻から 30 (既定)、60、または90分間、ユーザーが会議室をすばやく検索して予約することができます。 個人または1:1 の会話に対して、会議中の bot の範囲を示します。

[GitHub で取得する](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![書籍-a ルームのデモ](../assets/images/book-a-room.png)

## <a name="attendance-app"></a>出席アプリ

出席アプリは、チーム内でピン留めできる [ [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) ] タブです。 これは、通常、学習およびトレーニング環境などの設定で、プレゼンスを記録するように設計されています。 ユーザーは、過去30日間の参加をマークまたは編集したり、グループ全体または個々の出席者のレポートをまとめて表示したりできます。

[GitHub で取得する](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![出勤アプリデモ](../assets/images/attendance-app.png)

## <a name="associate-insights-app"></a>Insights アプリを関連付ける

アソシエイト insights は、顧客の意見、心理、認識を直接取得して送信するための、第一線ワーカーを支援する[パワーアプリ](/powerapps/maker/canvas-apps/embed-teams-app)テンプレートです。 Firstline ワーカーは、多くの場合、一対一の取引先担当者として顧客と協力することになります。 収集されたデータは、ビジネスチーム (たとえば、Power BI Teams タブを介して) によって共有および使用して、製品の改善や顧客のエクスペリエンスの向上に利用できます。

[GitHub で取得する](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![アプリケーションによって生成された分析情報のフィードバックビュー](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![App が生成した application insights の Power BI ビュー](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

参照したいアプリテンプレートのアイデアがあるかどうか。 お知らせ[ください](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)。
