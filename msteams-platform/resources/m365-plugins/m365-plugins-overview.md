---
title: Microsoft 365 プラグイン
description: Microsoft 365 プラグインの詳細
ms.topic: Microsoft 365 plugins
ms.localizationpriority: high
ms.author: Surbhigupta
ms.openlocfilehash: 3a1847a01687d2d363f29938ed589d3a12179c9c
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63454000"
---
# <a name="microsoft-365-plugins"></a>Microsoft 365 プラグイン

Microsoft 365 プラグインは、Moodle Web サイトと Teams 間の統合を提供します。 これらのプラグインを使用すると、ユーザーはコースコンテンツのスケジュール設定、配信、共同作業を簡単に行えます。 プラグインは、要件に従って独立して、またはパートナーシップで使用できます。

## <a name="plugin-list-and-labels"></a>プラグインのリストとラベル

次の表に、要件に基づいて使用するプラグインと GitHub ラベルのリストを示します。

<!--Old content of the table updated and revamped |Plugins to install |Description |GitHub label(s)|
|-----|-----|----|
|[**OpenID Connect**](#openid-connect)|Enable SSO for users who work using both Moodle and Microsoft Teams|auth_oidc|
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) |Create Teams instances for each course in Moodle, and sync faculty as owners, and students as team members|• auth_oidc </br> • local_o365|
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) </br> • [**Teams Theme**](#microsoft-365-teams-theme)| Remove Moodle blocks and extra chrome within the Moodle iframes for Teams, which applies while mapping courses to Teams instances | • auth_oidc </br> • local_o365 </br> • themeboost_o365teams |
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) </br> • [**Microsoft 365 Repository**](#microsoft-365-repository) |Leverage Microsoft 365 OneDrive content for file repositories to reduce storage needs in Moodle | • auth_oidc </br> * local_o365 </br> • repository_office 365|
|• [**OpenID Connect**](#openid-connect) </br> • [**OneNote**](#onenote-integration) </br> • [**OneNote Submissions**](#onenote-integration) </br> • [**OneNote Feedback**](#onenote-integration) | Enable OneNote to be used for assignment, submission and feedback |• auth_oidc </br> • local_onenote </br> • assignsubmission_onenote </br> • assignfeedback_onenote |  
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) • [**Microsoft 365 Repository**](#microsoft-365-repository) </br> • [**Microsoft Block**](#microsoft-365-repository) | Enable 365 quick access blocks within Moodle with links to Microsoft 365 collaboration services and install links for Microsoft Office | • auth_oidc </br> • local_o365 </br> • repository_office365 </br> • block_microsoft |
|[**Teams Meeting**](#teams-meetings) | Enable Atto editor in Moodle to create Teams meeting links |atto_teamsmeeting |
|[**oEmbed Filter**](#oembed-filter) | Enable video links in Moodle | Filter_oembed| -->

|インストールするプラグイン |説明 |GitHub ラベル|
|-----|-----|----|
|[**OpenID Connect**](#openid-connect)|Moodle と Teams の両方を使用して作業するユーザーに対して SSO を有効にします。|auth_oidc|
|[**Microsoft 365 の統合**](#microsoft-365-integration)|Moodle で各コースの Teams インスタンスを作成し、教職員を所有者として、学生をチーム メンバーとして同期します。|local_o365|
|[**Microsoft 365 リポジトリ**](#microsoft-365-repository) |Moodle のストレージのニーズを減らすために、ファイル リポジトリ の Microsoft 365 OneDrive コンテンツをサポートしています。| repository_office 365|
|[**Teams 会議**](#teams-meetings) |Moodle の Atto エディターで Teams 会議リンクを作成できるようにします。|atto_teamsmeeting |
|[**Teams テーマ**](#microsoft-365-teams-theme)| Teams の Moodle iframe 内の Moodle ブロックと余分なクロムを削除します。これは、コースを Teams インスタンスにマッピングするときに適用されます。| themeboost_o365teams |
|[**OneNote**](#onenote-integration)| OneNote を割り当て、提出、フィードバックに使用できるようにします。|local_onenote, assignsubmission_onenote および assignfeedback_onenote </br>|  
|[**Microsoft Block**](#microsoft-block) | Moodle 内の Microsoft 365 クイック アクセス ブロックを、Microsoft 365 コラボレーション サービスへのリンクを使って有効化し、Microsoft Office のリンクをインストールします。|block_microsoft |
|[**oEmbed Filter**](#oembed-filter) | Moodle でビデオ リンクを有効にする。|Filter_oembed|

Moodle LMS は、次のプラグインをサポートしています。

## <a name="openid-connect"></a>OpenID Connect

Open ID Connectプラグインを使用すると、ユーザーは、必要な仕様をサポートする Web サイトまたはツールを認証し、Microsoft Office 365 で シングル サインオン サポート (SSO) を提供します。 OpenID Connect プラグインは、教育機関の特定の要件を満たすために、次のサインイン オプションを提供します:

* ユーザーは、Office 365 にサインインせずに、メールやパスワードなどの Office 365 資格情報を入力して直接サインインしたり、Moodle のユーザー名とパスワード フィールドを使用してサインインできます。
* ユーザーは、Office 365 または Moodle ページの OpenID Connect プロバイダーを使用してサインインするためのリンクを選択できます。

次の図は、OpenID 接続ログイン ページを表しています:

:::image type="content" source="../../assets/images/MoodleInstructions/openid-connect.png" alt-text="open-id connect へのログイン" border="true":::

## <a name="microsoft-365-integration"></a>Microsoft 365 の統合

Microsoft 365 の統合は、複数の機能を備えた複数のアプリで構成されています。これにより、ユーザーは接続を維持し、必要に応じてさまざまな操作を実行できます。 このプラグインを使用すると、管理者は次の情報を確認できます:

* 適切な統合機能を確認します。
* Office 365 と Moodle の間でユーザーを同期します。
* ユーザーに必要なアクセス許可を構成します。
* コース ファイルの SharePoint Web サイトを設定します。

次の図は、Microsoft 365 統合セットアップ ページを表しています:

:::image type="content" source="../../assets/images/MoodleInstructions/365-integration.png" alt-text="Microsoft 365 の統合" border="true":::

### <a name="user-functions"></a>ユーザー機能

ユーザーは、Microsoft 365 統合を使用して次の操作を実行できます:

* すべての Microsoft 365 プラグイン統合の全体的な機能を確認します。
* Moodle と Office 365 ユーザーを比較する CSV ファイルをアップロードします。
* Azure AD アクセス許可の構成を確認します。

## <a name="microsoft-365-repository"></a>Microsoft 365 リポジトリ

Microsoft 365 リポジトリ プラグインを使用すると、ユーザーはコース ファイルを OneDrive に保存できます。 教職員は、OneDrive のコース ファイル セクションまたは自分の個人用スペースからリポジトリにファイルを追加できます。

Microsoft 365 リポジトリを使用すると、ユーザーは Moodle のデータ構造をシンプルにしながら、教育機関のファイル リポジトリとして使用できます。 Microsoft 365 リポジトリ プラグインには、次のサービスが用意されています:

* 教職員はコース ファイルを OneDrive に保存できます。 各コースには、OneDrive で作成された独自のフォルダーがあり、これにより、教職員は OneDrive のコース ファイル領域から、または自分の個人用スペースからファイルを追加できます。  
* コピーとして Moodle にファイルを追加するか、ファイルへのリンクを作成します。 リンクされたファイルは、新しいアプリケーション ウィンドウに表示されるか、Web ページに埋め込まれます。
* Moodle ファイル ピッカーを使用して OneDrive または SharePoint にファイルをアップロードする。

次の図は、Microsoft 365 統合ファイル リポジトリを表しています:

:::image type="content" source="../../assets/images/MoodleInstructions/microsoft-365- repository.png" alt-text="M365 リポジトリ"  border="true":::

## <a name="teams-meetings"></a>Teams 会議

Teams会議プラグインを使用すると、ユーザーは予定表、割り当て、フォーラム投稿、および利用可能時間に応じて Atto エディターで会議出席依頼を作成できます。

プラグインをインストールした後、教職員と学生は Moodle を使用してオーディオ会議またはビデオ会議を作成できます。これには、Microsoft 365 アカウントと Moodle のアクセス許可が必要です。

>[!NOTE]
>Teams 会議は Outlook または Teams カレンダーには表示されませんが、個々の学生名を teams 会議の招待に追加できます。

次の図は、Teams 会議サインイン ページを示しています。

:::image type="content" source="../../assets/images/MoodleInstructions/teams-meeting.png" alt-text="チーム会議にサインインする" border="true":::

## <a name="microsoft-365-teams-theme"></a>Microsoft 365 Teamsテーマ

Microsoft 365 Teams テーマ プラグインは、Moodle コースのホーム ページのカスタム ビューをユーザーに提供し、ユーザーが Teams 内の Moodle コースにアクセスしたときに表示できます。

テーマ プラグインを使用すると、ユーザーは次の機能を使用して統合された強化されたエクスペリエンスを利用できます。

* Microsoft Teams のテーマの変更 (既定、ダーク、ハイ コントラストなど) に適応します。
* コース アクティビティがフォーカスされます。
* Moodle ブロック、ナビゲーション、ヘッダー、フッターが削除されます。
* Microsoft Team ユーザー インターフェイス (UI) 要素が提供されます。

次の図は、ユーザーが設定した Teams テーマを示しています。

:::image type="content" source="../../assets/images/MoodleInstructions/teams-theme.png" alt-text="Microsoft Teamsテーマ" border="true":::

## <a name="onenote-integration"></a>OneNote の統合

OneNote 統合プラグインは、ノートブック、セクション、ページを参照するためのオプションをユーザーに提供します。これにより、課題が送信され、教職員が OneNote の対応する課題に関して必要なフィードバックを提供します。 OneNote では、テストやリンク以外の機能を追加したり、デジタル ペン、写真やビデオ メディア、グループとの共同編集を使用してモバイルに機能を拡張したりすることで、ユーザー エクスペリエンスも向上します。

OneNote 統合は、テキスト、グラフィックス、オーディオ リポジトリへのアクセスに役立ちます。 プラグインには、次の利点があります:

* ノートブック、セクション、ページの閲覧を包含し、学生が課題に取り組み、OneNote でそれらの課題に関するフィードバックを提供できるようにします。
* メモ、課題、フィードバックのデジタル バインダーを組み合わせて、参照とレビューを行います。
* テキストやリンク以外の下書き機能を拡張し、デジタル ペン、写真またはビデオ メディア、グループとの共同編集を使用してモバイルの使用を拡張します。
* 各課題の提出とフィードバック ページを教職員のアカウントに含めます。 こうしたものを Moodle 内に保存すると、HTML と関連する画像のコピーが zip ファイルにパッケージ化されます。

> [!NOTE]
> 提出イベントまたはフィードバック イベントは、学生が登録した各コースのセクションを含む OneNote の作成をトリガーします。

## <a name="microsoft-block"></a>Microsoft ブロック

Microsoft ブロック プラグインを使用すると、ユーザーは、SharePoint ファイルの場所にアクセスし、OneNote ノートブックで申請用にコースを表示し、Office 365 統合のユーザー設定を変更できます。 管理者は、すべてのコース ページに表示されるブロックを構成できます。

Microsoft ブロックは、Microsoft 365 統合機能を変更し、その多数のリソースにアクセスするためのユーザー インターフェイスを提供することで、ユーザー エクスペリエンスを強化します。 管理者は、変更された変更を各コース ページに表示するブロックを構成できます。 このブロックを使用すると、ユーザーは次のアクティビティを実行できます:

* コースの SharePoint ファイルの場所と OneNote ノートブックにアクセスする。
* 提出用に OneNote ノートブックでコースを表示する。
* Outlook カレンダーの同期を構成する。
* Office 365 統合への接続を管理する。
* 個人用 Office 365 統合のユーザー設定をカスタマイズする。

次の図は、Microsoft ブロック ユーザー インターフェイスを示しています:

:::image type="content" source="../../assets/images/MoodleInstructions/microsoft-block-1.png" alt-text="Microsoft ブロック" border="true":::

## <a name="oembed-filter"></a>oEmbed フィルター

oEmbed フィルター プラグインは、Moodle 内の外部 HTML コンテンツの包含を簡略化することで、ユーザー エクスペリエンスを簡素化し、強化します。 oEmbed フィルターの利点を次に示します。 

* HTML ページにビデオを埋め込む時間を短縮します。
* 複数のビデオ コンテンツ プロバイダーの埋め込みを有効にします。
* サポートされているサービスからコードをコピーして埋め込む方法を迅速に行います。
* API キーなしでビデオの埋め込みを許可します。

次の図は、Moodle 内への外部 HTML コンテンツの包含を示しています:

:::image type="content" source="../../assets/images/MoodleInstructions/oEmbed-filter.png" alt-text="oEmbed フィルター ページ" border="true":::

## <a name="see-also"></a>関連項目

* [Moodle のパートナー アプリ](../partner-apps-for-moodle.md)
* [Moodle に関するよく寄せられる質問](../faqs.md)