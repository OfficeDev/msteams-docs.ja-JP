---
title: Microsoft Teams 開発者向けドキュメント - 用語集
description: 開発者向けドキュメント Microsoft Teams 用語集
ms.localizationpriority: high
ms.topic: reference
keywords: Microsoft Teams 開発者定義
ms.openlocfilehash: 25d5cb5828671ffe464b9cd66a5d8de97db5ecbf
ms.sourcegitcommit: 3d7b34e7032b6d379eca8f580d432b365c8be840
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/18/2022
ms.locfileid: "62898076"
---
# <a name="glossary"></a>用語集

Teams 開発者向けドキュメントで使用される一般的な用語と定義。


## <a name="a"></a>A

| 用語 | 定義 |
| --- | --- |
| [アクション コマンド](../messaging-extensions/how-to/action-commands/define-action-command.md) | ポップアップを使用して情報を収集または表示するメッセージング拡張機能アプリの種類。 <br>**関連情報**: 「[メッセージング拡張機能](#m); [検索コマンド](#s) |
| [アダプティブ カード](../task-modules-and-cards/what-are-cards.md) | ボットまたはメッセージング拡張機能によって会話に追加されたアクション可能なコンテンツ スニペット。 リッチ コミュニケーションのために、これらのカードでテキスト、グラフィックス、ボタンを使用します。 |
| [匿名ユーザー](../apps-in-teams-meetings/meeting-app-extensibility.md#user-types-in-a-meeting) | Azure AD ID を持っておらず、テナントとフェデレーションされていない Teams 会議の参加者の種類。 これらは、会議の外部ユーザーのようなものです。 <br>**関連情報**: [フェデレーション ユーザー](#f) |
| [アプリ カタログ](../toolkit/publish.md) | 組織の内部使用のために SharePoint アプリと Office アプリを格納するサイト。 <br>**関連情報**: [SPFx](#s) |
| [アプリ マニフェスト](../resources/schema/manifest-schema.md) | Teams アプリ マニフェストは、アプリが Microsoft Teams 製品にどのように統合されるかを説明します。 マニフェストは、最新の[マニフェスト スキーマ](https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json)に適合している必要があります。 |
| [アプリ パッケージ](../concepts/build-and-test/apps-package.md) | Teams アプリ パッケージは、アプリ マニフェスト ファイル、色アイコン、アウトライン アイコンを含む zip ファイルです。 |
| [アプリのアクセス許可](../concepts/device-capabilities/browser-device-permissions.md#enable-apps-device-permissions) | デバイスのアクセス許可を有効にする Teams アプリのオプション。 アプリのマニフェスト ファイルで、アプリにデバイスのアクセス許可が必要であると宣言されている場合にのみ使用できます。 <br> **関連情報**: デバイスのアクセス許可 |
| [アプリのスコープ](../concepts/design/app-structure.md) | ユーザーがあなたのアプリを使用できる Teams の領域。 アプリには、個人用、チャネル、チャット、会議など、1 つまたは複数のスコープを設定できます。 Teams アプリは、複数のスコープにわたって存在できます。 |
| [App Studio](../concepts/build-and-test/app-studio-overview.md) | 独自の Microsoft Teams アプリの作成または統合を開始するアプリ。 開発者ポータルに進化しました。 <br> **関連情報**: [開発者ポータル](#d) |
| アプリ トレイ | Teams モバイル アプリの下部バーにあるアプリケーション トレイ。 開いているが現在使用されていない、またはアクティブではないすべてのアプリが収集されます。 <br>**関連情報**: [Teams Mobile](#t) |
| [Azure リソース](../toolkit/provision.md) | Teams アプリが Azure デプロイに使用できる Azure 経由で利用できるサービス。 ストレージ アカウント、Web アプリ、データベースなどです。 |
| [Azure Active Directory](../tabs/how-to/authentication/auth-tab-aad.md) | Microsoft クラウドベースの、ID およびアクセス管理サービスです。 認証されたユーザーが内部および外部の Azure リソースにアクセスするのに役立ちます。 |
| [認証](../concepts/authentication/authentication.md) | アプリの使用状況についてユーザー アクセスを検証するプロセス。 これは、Microsoft Graph API または Web ベースの認証を使用して行うことができます。 <br> **関連情報**: [ID プロバイダー](#i); [SSO](#s) |
| [認証フロー](../concepts/authentication/authentication.md#web-based-authentication-flow) | Teams には、アプリを使用するためにユーザーを認証する認証フローが 2 つあります。Web ベースの認証と OAuthPrompt フローです。 |
|

## <a name="b"></a>B

| 用語 | 定義 |
| --- | --- |
| [Blazor](../get-started/get-started-overview.md) | 開発者が C# と HTML を使用して Web アプリを作成できるようにする、無料のオープン ソース Web フレームワーク。 Microsoft によって開発されています。 |
| [Bicep](../toolkit/provision.md) | 宣言型言語。つまり、要素は任意の順序で表示できます。 命令型言語とは異なり、要素の順序はデプロイの処理方法に影響しません。 |
| [ボット](../bots/what-are-bots.md) | ボットは、プログラムされた反復タスクを実行するアプリです。 <br> **関連情報**: [会話型ボット](#c); [チャット ボット](#c) |
| [ボット エミュレーター](../bots/how-to/debug/locally-with-an-ide.md#use-the-bot-emulator) | ローカルまたはリモートでボットをテストおよびデバッグできるデスクトップ アプリケーション。 |
| [Bot Framework](../bots/bot-features.md) | C#、Java、Python、JavaScript を使用してボットを作成するために使用される豊富な SDK。 Bot Framework に基づくボットがある場合は、Teams で動作するようにボットを変更できます。 |
|

## <a name="c"></a>C

| 用語 | 定義 |
| --- | --- |
| [通話ボット](../bots/calls-and-meetings/calls-meetings-bots-overview.md) | 音声通話またはビデオ通話とオンライン会議に参加するボット。 <br> **関連情報**: [チャット ボット](#c); [会議ボット](#m) |
| [機能](../toolkit/add-capability.md) | アプリ ユーザーと対話するためにアプリに組み込むことができる Teams 機能。 アプリの機能は、アプリのニーズに合わせて Teams を拡張するために使用されます。 アプリには、タブ、ボット、メッセージング拡張機能などの 1 つ以上のコア機能が含まれる場合があります。 <br>**以下も参照してください**: [デバイス機能](#d); [メディア機能](#m) |
| [チャット ボット](../bots/how-to/conversations/conversation-basics.md) | ボットは、チャットボットまたは会話ボットとも呼ばれます。 これは、カスタマー サービスやサポート スタッフなどのユーザーが単純で反復的なタスクを実行するアプリです。 <br> **以下も参照してください**: [会話ボット](#c) |
| チャネル | チームがメッセージ、ツール、ファイルを 1 か所で共有できます。 チームワークとコミュニケーションにチャネルを使用できます。 <br>**関連情報**: [会話](#c) |
| [クライアント シークレット](../bots/how-to/authentication/add-authentication.md) | クライアントシークレット/パスワード、または証明書である公開キーまたは秘密キーのペア。 ネイティブ アプリには必要ありません。 <br> **関連情報**: [ボット](#b) |
| [クラウド リソース](../toolkit/add-resource.md) | Teams アプリが使用できるインターネットを経由してクラウド上で利用できるサービス。 ストレージ アカウント、Web アプリ、データベースなどです。 |
| [コラボレーション アプリ](../concepts/extensibility-points.md) | ユーザーが他のユーザーと共同作業ワークスペースで作業するための機能を備えたアプリ。 <br> **関連情報**: [スタンドアロン アプリ](#s) |
| [拡張機能の作成](../resources/schema/manifest-schema.md#composeextensions) | メッセージング拡張機能を参照するアプリ マニフェスト (`composeExtensions`) のプロパティ。 これは、拡張機能を認証するか、続行するように構成する必要がある場合に使用されます。 <br>**関連情報**: [アプリ マニフェスト](#a); [メッセージング拡張機能](#m) |
| [コマンド ボックス](../resources/schema/manifest-schema.md) | Teams コマンド ボックスからメッセージング拡張機能を呼び出すように構成できるアプリ マニフェスト (`commandBox`) のコンテキストの種類。 |
| [Connector](../webhooks-and-connectors/what-are-webhooks-and-connectors.md) | これを使用して、ユーザーは Web サービスから通知とメッセージを受信するようにサブスクライブできます。 コネクタにより、サービスが Teams チャネルにメッセージを投稿するための HTTPS エンドポイントが通常はカードの形式で公開されます。 <br> **関連情報**: [Webhook](#w) |
| 会話 | Microsoft Teams アプリ (タブまたはボット) と 1 人以上のユーザーの間で送信される一連のメッセージ。 会話には、チャネル、個人用、グループ チャットの 3 つのスコープを設定できます。 <br>**関連情報**: [1 対 1 チャット](#o); [グループ チャット](#g); [チャネル](#c) |
| [会話型ボット](../bots/how-to/conversations/conversation-messages.md) |  これにより、ユーザーはテキスト、対話型カード、タスク モジュールを使用して Web サービスと対話できます。 <br>**関連情報** [チャット ボット](#c) |
|


## <a name="d"></a>D

| 用語 | 定義 |
| --- | --- |
| [ディープ リンク](../concepts/build-and-test/deep-links.md) | Teams アプリでは、Teams 内の情報や機能へのディープ リンクを作成したり、ユーザーをあなたのアプリ内のコンテンツに移動させたりするのに役立ちます。 |
| [Teams の開発者ポータル](../concepts/build-and-test/teams-developer-portal.md) | Microsoft Teams アプリを構成、配布、管理するための主要なツール。 開発者ポータルを使用すると、アプリで同僚と共同作業したり、ランタイム環境を設定したり、その他多くのことをしたりすることができます。 |
| [開発者向けプレビュー](../resources/dev-preview/developer-preview-intro.md) | Microsoft Teams の未リリース機能への早期アクセスを提供する開発者向けのパブリック プログラム。 これにより、Microsoft Teams アプリに含める候補として今後導入予定の機能を検索およびテストすることができます。 |
| 展開 | アプリケーションのバックエンドコードとフロントエンド コードをアップロードするプロセス。 デプロイ時に、アプリのコードがプロビジョニング中に作成したリソースにコピーされます。 <br>**関連情報**: [プロビジョニング](#p) |
| [デバイス機能](../concepts/device-capabilities/device-capabilities-overview.md) | カメラ、マイク、バーコード スキャナー、フォト ギャラリーなどの組み込みデバイスをモバイルまたはデスクトップで使用できます。 Microsoft Teams JavaScript クライアント SDK で利用可能な専用 API を使用して、モバイルまたはデスクトップで次のデバイス機能にアクセスできます。 <br>**関連情報**: [機能](#c); [メディア機能](#m); [場所機能](#l) |
| [デバイス許可](../concepts/device-capabilities/browser-device-permissions.md) | アプリで構成できる Teams アプリ設定。 これを使用して、アプリがネイティブ デバイス機能にアクセスして利用するためのアクセス許可を要求します。 Teams の設定でデバイスのアクセス許可を管理できます。 <br>**関連情報**: [アプリのアクセス許可](#a) |
| [開発環境](../toolkit/teamsfx-multi-env.md#create-a-new-environment) | Teams Toolkit によって既定で作成される開発環境の種類。 リモート環境またはクラウド環境の構成を表します。 プロジェクトには複数のリモート環境を含めることができます。 Teams Toolkit を使用して、より多くの開発環境をプロジェクトに追加できます。 <br>**関連情報** [環境](#e); [ローカル環境](#l) |
| [DevTools](../tabs/how-to/developer-tools.md) | ブラウザーの Devtools は、コンソール ログの表示、ランタイム ネットワーク要求の表示または変更、コードへのブレークポイントの追加 (JavaScript)、Teams アプリの対話型デバッグの実行に使用されます。 この機能は、開発者プレビューが有効にされた後、デスクトップ クライアントと Android クライアントでのみ使用できます。 |
| [動的検索](../task-modules-and-cards/cards/dynamic-search.md#dynamic-typeahead-search) | 大規模なデータ セットからデータを検索して選択するのに役立つアダプティブ カードの検索機能。 ユーザーが検索文字列を入力すると、選択肢をフィルターで除外できます。 <br>**関連情報**: [静的検索](#s) |
|


## <a name="e"></a>E

| 用語 | 定義 |
| --- | --- |
| [E5 開発者アカウント](../toolkit/accounts.md) | Microsoft 365 を拡張するアプリを構築するための E5 開発者サブスクリプション。 管理者を含めて最大 25 個のユーザーライセンスを含めることができますが、開発目的のみの使用となります。  <br>**関連情報**: [Microsoft 365 アカウント](#m) |
| [エントリ ポイント](../concepts/app-fundamentals-overview.md) | チーム、チャネル、チャットなど、ユーザーがあなたのアプリを使用できる Team アプリのアクセス ポイント。 |
| [環境](../toolkit/teamsfx-multi-env.md) | アプリ プロジェクトに対して複数の開発環境を作成して使用できるようにする Teams Toolkit の機能。 Teams Toolkit が既定で作成する開発環境は、ローカル環境と開発環境の 2 つです。 <br>**関連情報**: [ローカル環境](#l); [開発環境](#d) |
|


## <a name="f"></a>F

| 用語 | 定義 |
| --- | --- |
| [フェデレーション ユーザー](../apps-in-teams-meetings/meeting-app-extensibility.md#user-types-in-a-meeting) | 外部で会議に招待されている Teams アプリ会議のユーザーの種類。 このユーザーには、承認された Teams パートナーによってフェデレーションされた有効な資格情報があります。 外部ユーザーとも呼ばれます。 <br>**関連情報**: [匿名ユーザー](#a) |
|

## <a name="g"></a>G

| 用語 | 定義 |
| --- | --- |
| [Graph API](../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) | Microsoft Cloud サービス リソースへのアクセスを可能にするMicrosoft Graph 用の RESTful Web API です。 <br>**関連情報**: [Microsoft Graph エクスプローラー](#m) |
| [グループ チャット](../resources/bot-v3/bot-conversations/bots-conversations.md) | @mention を使用してボットを呼び出すことで、ユーザーがグループ設定でボットとチャットできるチャット機能。 <br>**関連情報**: [1 対 1 のチャット](#o); [チャット ボット](#c) |
|


## <a name="i"></a>I

| 用語 | 定義 |
| --- | --- |
| [ID プロバイダー](../concepts/authentication/configure-identity-provider.md) | ユーザーに資格情報を格納して提供するエンティティ。 ユーザーは ID プロバイダーにも登録できます。  <br>**関連情報**: [認証](#a) |
| [着信 Webhook](../webhooks-and-connectors/how-to/add-incoming-webhook.md) | これにより、外部アプリは Teams チャネルでコンテンツを共有できます。 これらの Webhook は、追跡および通知ツールとして使用されます。 <br>**関連情報**: [Webhook](#w); [発信 Webhook](#o) |
| [会議中のアプリ エクスペリエンス](../apps-in-teams-meetings/meeting-app-extensibility.md#in-meeting-app-experience) | Teams 会議ライフサイクルのステージ。 会議中のアプリ エクスペリエンスを使用すると、アプリと会議内ダイアログ ボックスを使用して、会議中に参加者とのやり取りを行うことができます。 <br>**関連情報**: [会議のライフサイクル](#m) |
|


## <a name="l"></a>L

| 用語 | 定義 |
| --- | --- |
| [リンク展開](../messaging-extensions/how-to/link-unfurling.md) | メッセージ作成領域に貼り付けられたリンクを展開するためにメッセージング拡張機能と会議で使用される機能。 リンクが展開され、リンクに関する追加情報が アダプティブ カード または会議ステージ ビューに表示されます。 |
| [ローカル環境](../toolkit/teamsfx-multi-env.md#create-a-new-environment) | Teams Toolkit によって作成される既定の開発環境。  <br>**関連情報**: [環境](#e); [開発環境](#d) |
| [ローカル ワークベンチ](../sbs-gs-spfx.yml) | SPFx を使用して作成された Visual Studio Code で Teams アプリを実行およびデバッグするための既定のオプション。 <br>**関連情報**: [Workbench](#w); [Teams ワークベンチ](#t) |
| [場所機能](../concepts/device-capabilities/location-capability.md) | アプリと統合して、アプリ ユーザーの場所を把握し、コラボレーション エクスペリエンスを強化できるデバイス機能。 この機能は現在、Teams モバイル クライアントでのみ使用できます。 <br>**関連情報**: [機能](#c); [メディア機能](#m); [デバイス](#d); [Teams モバイル](#t) |
| [低コード アプリ](../samples/teams-low-code-solutions.md) | コーディングをほとんどまたはまったく必要とせず、迅速に開発および展開できる Microsoft Power Platform を使用して最初から構築されたカスタム Teams アプリ。 |
|


## <a name="m"></a>M

| 用語 | 定義 |
| --- | --- |
| [メディア機能](../concepts/device-capabilities/mobile-camera-image-permissions.md) | カメラやマイクなど、Teams アプリと統合できるネイティブ デバイス機能。 <br>**関連情報**: [機能](#c); [デバイス機能](#d) |
| [会議ボット](../bots/calls-and-meetings/calls-meetings-bots-overview.md) | リアルタイムの音声、ビデオ、画面共有を使用して Teams の通話や会議と対話するボット。 <br>**関連情報**: [通話ボット](#c); [チャット ボット](#c) |
| [会議のライフサイクル](../apps-in-teams-meetings/meeting-app-extensibility.md#meeting-lifecycle) | これは、会議前、会議中、および会議後のアプリ エクスペリエンスに及びます。 会議のライフサイクルの各段階で、タブ、ボット、メッセージング拡張機能を統合できます。 <br>**関連情報**: [会議中エクスペリエンス](#i) |
| [会議ステージ](../sbs-meetings-stage-view.yml) | 会議拡張機能アプリの機能。 会議中にすべての参加者がアクセスできる共有スペースです。 これは、参加者がリアルタイムでアプリ コンテンツと対話して共同作業するのに役立ちます。 <br>**関連情報**: [ステージ ビュー](#s) |
| [メッセージング拡張機能](../messaging-extensions/what-are-messaging-extensions.md) | メッセージング拡張機能は、アプリのコンテンツを挿入したり、メッセージを操作したりするためのショートカットです。 会話から離れることなく、メッセージング拡張機能を使用できます。 <br>**関連情報**: [検索コマンド](#s); [アクション コマンド](#a) |
| [会議の拡張機能](../apps-in-teams-meetings/design/designing-apps-in-meetings.md) | ホワイトボード、ダッシュボードなど、会議のライフサイクル中に生産性を高めるために使用するように設計されたアプリ。 |
| [Microsoft 365 アカウント](../toolkit/accounts.md#microsoft-365-account) | Microsoft 365 アカウントには、25 のユーザー ライセンスを含めることができますが、開発目的のみの使用となります。 |
| [Microsoft 365 開発者プログラム](../toolkit/accounts.md#join-microsoft-365-developer-program) | Microsoft 365 開発者プログラムは、Microsoft 365 を拡張するアプリの構築に役立ちます。 |
| [Microsoft Graph Explorer](../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) | Microsoft 365 のデータとインテリジェンスへのゲートウェイ。 Microsoft 365、Windows 10、および Enterprise Mobility + Security のデータにアクセスできる統合されたプログラミング モデルが用意されています。 |
| [Microsoft Teams](../overview.md) | Microsoft Teams は、チームがリモートで共同作業を行うのに役立つグループ コラボレーション ソフトウェアです。 |
| [Microsoft Teams プラットフォーム](../concepts/app-fundamentals-overview.md) | Microsoft Teams 開発者プラットフォームを使用すると、開発者は独自のアプリやサービスを Teams と簡単に統合できます。 |
| [Microsoft Teams UI ライブラリ](../concepts/design/design-teams-app-ui-templates.md#microsoft-teams-ui-library) | Microsoft Teams UI ライブラリは、個々の Teams UI テンプレートと関連コンポーネントをブラウザーで表示およびテストするのに役立ちます。 |
| [Microsoft Teams UI ツールキット](../concepts/design/design-teams-app-ui-templates.md#microsoft-teams-ui-library) | Microsoft Teams UI Kit には、Teams アプリを構築するために特別に設計されたコンポーネントとパターンが含まれています。 |
|


## <a name="o"></a>O

| 用語 | 定義 |
| --- | --- |
| [Office 365 コネクタ](../webhooks-and-connectors/how-to/connectors-creating.md) | 受信 Webhook のカスタム構成ページを作成し、Teams アプリの一部としてパッケージ化できます。 主に Office 365 コネクタ カードを使用してメッセージを送信し、それらに限られたカード アクションのセットを追加できます。 |
| [送信 Webhook](../webhooks-and-connectors/how-to/add-outgoing-webhook.md) | 送信 Webhook はボットとして機能し、@mention を使用してチャネル内のメッセージを検索します。 外部 Web サービスに通知を送信し、カードや画像などの豊富なメッセージで応答します。 <br>**関連情報**: [Webhook](#w); [着信 Webhook](#i) |
| [Outlook チャネル](../m365-apps/extend-m365-teams-message-extension.md#add-an-outlook-channel-for-your-bot) | ユーザーが Microsoft Outlook から操作できるようにする Teams メッセージング拡張機能アプリの機能。 |
| [1 対 1 のチャット](../resources/bot-v3/bot-conversations/bots-conv-personal.md) | Teams 個人用ボット アプリと 1 人のユーザー間のチャットの種類。 <br>**関連情報**: [グループ チャット](#g); [チャット ボット](#c) |
|


## <a name="p"></a>P

| 用語 | 定義 |
| --- | --- |
| [ユーザー選択ウィンドウ](../task-modules-and-cards/cards/people-picker.md) | ユーザーを検索して選択するための Teams プラットフォームのネイティブ コントロールで、Web アプリ、アダプティブ カードなどと統合できます。 |
| [個人用アプリ](../concepts/design/personal-apps.md) | 個人用アプリは、個人用スコープを持つ Teams アプリケーションです。 1 人のユーザーとの対話に重点を置きます。 埋め込み Web エクスペリエンスを提供するユーザーまたは個人用タブとの 1 対 1 の会話に参加する会話ボット、またはその両方を行うことができます。 <br>**関連情報**: [共有アプリ](#s) |
| [Power Virtual Agents](../bots/how-to/add-power-virtual-agents-bot-to-teams.md) | チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できるリッチで会話型のチャット ボットを作成できるコード不要のガイド付きグラフィカル インターフェイス ソリューション。 |
| [プロアクティブ メッセージ](../bots/how-to/conversations/send-proactive-messages.md) | ウェルカム メッセージ、通知、スケジュールされたメッセージなど、ユーザーからの要求に応答していないボットによって送信されたメッセージ。 |
| [プロビジョニング](../toolkit/provision.md) | Azure と Microsoft 365 でアプリ用にリソースを作成するプロセスです。ただし、コード (HTML、CSS、JavaScript など) はリソースにコピーされません。 これは、展開の前提条件です。 <br>**関連情報**: [展開](#d) |
|


## <a name="r"></a>R

| 用語 | 定義 |
| --- | --- |
| [速度制限中](../bots/how-to/rate-limit.md) | メッセージの数が十分であり、スパムとして表示されないように、メッセージを特定の最大頻度に制限する方法。 |
| [ロールベースのビュー](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/user-specific-views.md) | ユーザーのアクセス許可レベルに応じてタブ エクスペリエンスが異なる可能性があるタブの機能。 |
| [RSC アクセス許可](../graph-api/rsc/resource-specific-consent.md) | チーム所有者は、リソース固有の同意 (RSC) アクセス許可機能を使用して、ボット アプリが @mentioned されることなくチーム内のチャネル間でメッセージを受信できるようにする必要があります。 |
|


## <a name="s"></a>S

| 用語 | 定義 |
| --- | --- |
| [検索コマンド](../messaging-extensions/how-to/search-commands/define-search-command.md) | ユーザーが外部システムを検索し、カードを使用して検索結果をメッセージに含めることができるメッセージング拡張機能アプリの種類。 <br>**関連情報**: [メッセージング拡張機能](#m); [アクション コマンド](#a) |
| [シーケンシャル ワークフロー](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/sequential-workflows.md) | ボットがユーザー応答に基づいてユーザーとの会話を実行できるようにするワークフロー。 |
| [共有アプリ](../concepts/extensibility-points.md#shared-app-experiences) | ユーザーが共同作業や対話を行うことができるチーム、チャネル、またはチャットに存在するアプリ。 <br>**関連情報:** 個人用アプリ |
| [SharePoint サイト コレクション](../sbs-gs-spfx.yml) | SharePoint アプリのコレクション サイト。 SharePoint サイトに SPFx ベースのアプリを展開するには、このサイトの管理者アカウントが必要です。 <br>**関連情報**: SPFx |
| [サイドロード](../toolkit/publish.md#publish-to-individual-scope-or-sideload-permission) | Teams アプリを配布する前に Teams 環境でテストするために Teams クライアントに読み込まれるプロセス。 |
| [SidePanel](../sbs-meetings-sidepanel.yml) | 開催者と発表者が異なるビューとアクションのセットを持つ会議のエクスペリエンスをカスタマイズできるようにする Teams 会議アプリの機能。 |
| [SPFx](../sbs-gs-spfx.yml) | SharePoint Framework (SPFx) は、Microsoft Teams と SharePoint 用のクライアント側ソリューションを構築するための開発モデルです。 |
| SSO | シングル サインオンの頭字語。ユーザーがソフトウェア プラットフォーム (Microsoft 365 など) の独立したサービスに 1 回だけサインインする必要がある認証方法。 その後、ユーザーは認証を再度実行しなくても、すべてのサービスにアクセスできます。 <br>**関連情報**: [認証](#a) |
| [ステージ ビュー](../sbs-meetings-stage-view.yml) | Teams で全画面表示で開き、タブとしてピン留めされたコンテンツをレンダリングできるユーザー インターフェイス コンポーネント。Teams 内で Web コンテンツを表示するために呼び出されます。 会議ステージと同じ *ではない* ことに注意してください。 <br>**関連情報**: [会議ステージ](#m) |
| [スタンドアロン アプリ](../samples/integrating-web-apps.md) | 1 ページまたは大規模で複雑なアプリ。 ユーザーは Teams でその一部の側面を使用できます。 <br>**関連情報**: [コラボレーション アプリ](#c) |
| [静的検索](../task-modules-and-cards/cards/dynamic-search.md) | ユーザーがアダプティブ カード ペイロードで事前に指定された値から検索できるようにする先行入力検索のメソッド。 <br>**関連情報**: [動的検索](#d) |
| [ストア検証ガイドライン](../concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) | アプリを Teams ストアに送信する前に検証するための Teams 固有のガイドラインのセット。 <br>**関連情報**: [Teams ストア](#t) |
|


## <a name="t"></a>T

| 用語 | 定義 |
| --- | --- |
| [Tab](../tabs/what-are-tabs.md) | タブは、マニフェストで宣言されたドメインを指す Microsoft Teams に埋め込まれた Teams 対応の Web ページです。 チーム、グループ チャット、または個人用アプリ内に追加できます。 |
| [タブ チャット](../tabs/how-to/conversational-tabs.md) | 動的タブでユーザーが優先会話エクスペリエンスを持つタブの種類。 |
| [タスク モジュール](../task-modules-and-cards/what-are-task-modules.md) | タスクを完了したり、ビデオを表示したり、ダッシュボードを表示したりするためのモーダル ポップアップを作成する Teams アプリの機能。 |
| [スレッド ディスカッション](../tabs/design/tabs.md#thread-discussion) | ユーザー間のチャネルまたはチャットに投稿された会話。 <br>**関連情報** [会話](#c); [チャネル](#c) |
| [Teams](../overview.md) | Microsoft Teams は、組織にとって最高のメッセージング アプリです。 リアルタイムのコラボレーションやコミュニケーション、会議、ファイルやアプリの共有ができるワークスペースです。 |
| [Teams ツールキット](../toolkit/teams-toolkit-fundamentals.md) | Microsoft Teams ツールキットを使用すると、Visual Studio Code 環境内で直接カスタムの Teams アプリを構築できます。  |
| [TeamsFx](../toolkit/teamsfx-cli.md) | TeamsFx は、Teams アプリケーションの開発を加速するテキスト ベースのコマンド ライン インターフェイスです。 これは TeamsFx CLI とも呼ばれます。|
| [TeamsFx SDK](../toolkit/teamsfx-sdk.md) | TeamsFx SDK は、TeamsFx ツールキットまたは CLI を使用してスキャフォールディングされたプロジェクトで事前構成されています。 |
| [Teams モバイル](../concepts/design/plan-responsive-tabs-for-teams-mobile.md) | Microsoft Teams はモバイル アプリとして利用できます。 |
| [Teams ストア](../concepts/deploy-and-publish/appsource/publish.md) | アプリを 1 か所でユーザーに提供するストアのランディング ページ。 アプリは、使用状況、業界などによって分類されます。 アプリは、ストアの検証ガイドラインに従い、Teams ストアを介してユーザーが利用できるようになる前に承認を取得する必要があります。  <br>**関連情報**: [ストア検証ガイドライン](#s) |
| [Teams ワークベンチ](../sbs-gs-spfx.yml) | SPFx と Teams ツールキットを使って作成された Teams アプリのビルドで使われる Visual Studio Code のワークビーチ。 <br>**関連情報**: [Workbench](#w); [ローカル ワークベンチ](#l) |
|


## <a name="u"></a>U

| 用語 | 定義 |
| --- | --- |
| [UI コンポーネント](../concepts/design/design-teams-app-basic-ui-components.md) | Teams アプリ開発では、Fluent UI コンポーネントを使用してアプリを最初からビルドできます。 |
| [UI テンプレート](../concepts/design/design-teams-app-ui-templates.md) | Teams アプリ開発では、Teams UI テンプレートを使用してアプリをすばやく設計できます。 |
| [アダプティブ カードのユニバーサル アクション](../task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) | プラットフォームやアプリケーション間でアダプティブ カードを実装する方法。 アクションを処理するための一般的なバックエンドとしてボットを使用します。 |
|


## <a name="v"></a>V

| 用語 | 定義 |
| --- | --- |
| [仮想アシスタント](../samples/virtual-assistant.md) | 堅牢な会話型ソリューションを作成できる Microsoft オープン ソース テンプレート。 |
|


## <a name="w"></a>W

| 用語 | 定義 |
| --- | --- |
| [Web サイトの URL](../tabs/design/tabs-mobile.md) | アプリ マニフェスト ファイル (`websiteUrl`) 内のプロパティ。アプリを組織の Web サイトまたは関連する製品のランディング ページにリンクします。 これは、Teams モバイル クライアントの必須の構成です。 <br>**関連情報**: [アプリ マニフェスト](#a); [Teams モバイル](#t) |
| [Web アプリ](../samples/integrate-web-apps-overview.md) | Web サーバー上で実行されるアプリ。 Microsoft Teams プラットフォームと統合できます。 |
| [Webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md) | これは、外部アプリとの統合に使用される Teams アプリの機能です。 <br>**関連情報**: 受信 Webhook; 発信 Webhook |
| [Web パーツ](../sbs-gs-spfx.yml) | Visual Studio Code と SharePoint Framework を使用して作成された Teams アプリでページまたはサイトを構築するために使用される UI コンポーネント。 <br>**関連情報**: [SPFx](#s) |
| [Workbench](../sbs-gs-spfx.yml) | タイトル バー、パネルなどの UI コンポーネントを含む全体的な Visual Studio Code UI。 <br>**関連情報**: [ローカル ワークベンチ](#l); [Teams ワークベンチ](#t) |

    
## <a name="y"></a>Y

| 用語 | 定義 |
| --- | --- |
| [YoTeams](../get-started/get-started-overview.md) | TypeScript と node.js に基づいて Microsoft Teams アプリケーションを構築するための開発ツールキット。 |
|
