---
title: Moodle のよく寄せられる質問
description: この記事では、Moodle LMS を使用しているときによく寄せられるいくつかの質問に対する回答を取得します。
ms.topic: Frequently asked questions on Moodle LMS
ms.localizationpriority: high
ms.author: Surbhigupta
ms.openlocfilehash: c617b3db7982e192db6cde9375be751e2cf2bf26
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558297"
---
# <a name="moodle-faq"></a>Moodle に関するよく寄せられる質問

Moodle LMS を使用する場合のいくつかの質問に対する回答を取得します。<br>

<br>

<details>

<summary><b>同期後に 1 つ以上のコース チームが作成されなかった場合はどうすればよいですか?</b></summary>

各 Moodle コースには、少なくとも 1 人の教員と 1 人の学生が Microsoft 365 AAD UPN アカウントに一致する必要があります。 同期が一致しない場合、チームを作成することはできません。

各チームのコース インスタンスには所有者が必要で、同期では教員が Teams ライセンスを所有していることを前提として、教員が所有者として設定されます。

<br>

</details>

<details>

<summary><b>Teams で作業を行う場合、Moodle ログイ ンページを削除するには、どうすればいいですか? シングル サインオン (SSO) を強制することはできますか?</b></summary>

ユーザーは、Moodle ログイン ページから複数のサインイン オプションを利用できます。

* Microsoft 365 の資格情報のみを使用して排他的にサインインするには、**強制リダイレクト** の構成設定を **auth_oidc プラグイン** 用に有効にします。 サービスが有効な場合、ユーザーは Microsoft サインイン ページを表示できます。
* Moodle ポータルに手動でサインインするには、[Moodle](https://moodle.org/login/index.php) を参照してください。

<br>

</details>

<details>

<summary><b>同期するユーザーを指定するにはどうすればよいですか? 私は、すべての Azure AD ユーザーを Moodle Web サイトと同期させたくありません。</b></summary>

**[ユーザーの資格情報の制限]** オプションを使用して、**local_o365** プラグインの構成オプションを同期することでユーザーを指定します。 **フィルター** の左側にあるドロップダウン メニューには、国、会社名、言語などのオプションがあります。

> [!TIP]
> 動的な Microsoft 365 グループを作成して、複数のプロファイル プロパティ内で **フィルター** オプションを有効にします。

次の画像は、ユーザー作成の制限オプションを示しています。

:::image type="content" source="../assets/images/MoodleInstructions/faq-2.png" alt-text="同期":::

:::image type="content" source="../assets/images/MoodleInstructions/faq-3.png" alt-text="Azure AD":::

<br>

</details>

<details>

<summary><b>教員が Teams にコースを同期させることができるようにしますか? コースの同期を制御できるのは、Moodle 管理者だけですか?</b></summary>

既定では、Moodle 管理者だけが同期を構成できます。 チーム所有者はコースがチームに同期されるかどうかを制御することができ、**[コースでコース同期の構成を許可する]** が有効になっています。 この場合、チームの所有者は教員です。 このブロックは、適切な所有者権限を持つ個人に構成オプションを表示します。

<!-- For more information, see Microsoft 365 block within the Moodle course interface. -->

次の画像は、**[コースでコース同期の構成を許可する]** オプションを示しています。

:::image type="content" source="../assets/images/MoodleInstructions/faq-4.png" alt-text="管理者":::

次の画像は、コースの同期を示しています。

:::image type="content" source="../assets/images/MoodleInstructions/faq-5.png" alt-text="同期":::

<br>

</details>

<details>

<summary><b>ドキュメントに従いましたが、ユーザーアカウントが AAD と Moodle を同期できません。どうすればいいですか?</b></summary>

この問題は、トラブルシューティングの最終段階として、ユーザーが **デルタ トークンのクリーンアップ** を実行する前に解決できます。

次の表に、実行およびチェックするアクションと依存関係を示します。

| 依存関係 | Action | Reference|
|-------|------------|----------|
| 安定版| Moodle のバージョンが **安定** として一覧表示されているのを確認します。| 詳細については、「[バージョン サポート](https://docs.moodle.org/dev/Releases#Version_support)」を参照してください。|
|アクセス許可| Azure アプリケーションが同期を実行するのに必要なアクセス許可があることを確認します。| 詳細については、「[Microsoft Graph のアクセス許可](https://docs.moodle.org/311/en/Microsoft_365#Permissions)」を参照してください。|
| 完全同期| **[各実行の完全な同期を実行する]** が有効になっているかを確認し、**Azure AD を使用してユーザーと同期** する **タスク ログ** を確認します。| 詳細については、「[完全同期を有効にする](https://docs.moodle.org/311/en/local_o365)」を参照してください。</br>詳細については、「[タスク ログの確認](https://docs.moodle.org/311/en/local_o365#Sync_users_with_Azure_AD)」を参照してください。 |
|トークンの更新|local_o365 プラグインで **[ユーザー同期デルタ トークン]** をクリーンアップします。| 詳細については、「[トークンの更新](https://docs.moodle.org/38/en/Office365)」を参照してください。|
<!-- |トークンの更新|local_o365 プラグインで **[ユーザー同期デルタ トークン]** をクリーンアップする| {moodle_url}\local_o365\acp.php?Mode=maintenance_cleandeltatoken| -->
<br>

</details>

<details>

<summary><b>ほとんどのユーザーは問題なくサインインできますが、1 人以上のユーザーが Microsoft 365 資格情報を使用してサインインできません。この不整合の原因は何ですか?</b></summary>

Microsoft 365 資格情報を使用して署名できないユーザーに関する不整合の理由は、同期する際のユーザー マッピング操作に関連する可能性があります。 この問題を解決するには、以下の手順を実行します。

* Moodle のユーザ認証タイプが **OpenID** であるかどうかを確認します。
* Moodle の **ユーザー名** が AAD ユーザ名と一致するかどうかを確認します。
* **トークンの問題** をクリーンアップしてもう一度お試しください。
* ユーザーが Azure アプリケーションにアクセスするための **アクセス許可** を持っているかどうかを確認します。

<br>

</details>

<details>

<summary><b>すべてのユーザーが、Microsoft 365 の資格情報を使用してサインインすることができません。これを解決するにはどうすればよいですか?</b></summary>

起動時にサインインできなかったユーザーは、問題を報告し、アプリケーションの **クライアント シークレット** が期限切れになっていないことを確認する必要があります。

次の画像は、ユーザーが Microsoft 365 資格情報を使用して署名する際に表示されるエラー メッセージです。

:::image type="content" source="../assets/images/MoodleInstructions/faq-6.png" alt-text="レポートの問題":::

次の画像は、Azure Portal のエラーを示しています。

:::image type="content" source="../assets/images/MoodleInstructions/faq-7.png" alt-text="Azure portal":::

**クライアント シークレット** の期限が切れている場合は、新しい **クライアント シークレット** を生成し、ページで検出した構成を更新する必要があります。 ユーザーは **クライアント シークレット** が更新された後に再度サインインすることができますが、再プロビジョニングには最大 24 時間かかる可能性があります。

<br>

</details>

<details>

<summary><b>コースにリンクされたチーム インスタンスを変更するにはどうすればよいですか?</b></summary>

管理者は **[Teams 接続の管理]** ページ経由で、コースに関連するチーム インスタンスを変更できます。 変更するコースの横にある **[接続]** を選択し、Teams インスタンスを選択します。 コースリセットを使用してチームをアーカイブすると、以前のチームにリンクさせることができます。

次の画像は、Teams インスタンスを示します。

:::image type="content" source="../assets/images/MoodleInstructions/faq-8.png" alt-text="Teams インスタンス":::

<br>

</details>

<details>

<summary><b>Atto エディター内に Atto Teams 会議の統合が表示されない場合はどうすればよいですか?</b></summary>

Atto エディター内で Teams アイコンを表示する **ツールバー構成** でアイコン参照が見つからない場合、ユーザーに Atto Teams 会議の問題が発生している可能性があります。 ユーザーは、リンク アイコンの右側に Teams 会議アイコンを追加する必要があります。

* プラグインをインストールします。
* **Teams 会議** を使用して **ツールバー構成** を更新します。

次の画像は、ツールバーの構成を調整した後のツールバー アイコンを示します。

:::image type="content" source="../assets/images/MoodleInstructions/faq-9.png" alt-text="ツール バー":::

:::image type="content" source="../assets/images/MoodleInstructions/faq-10.png" alt-text="リンク アイコン":::

Atto ツールバーの編集に関する詳細については、以下を参照してください。

* [Atto editor-ModdleDocs](https://docs.moodle.org/311/en/Atto_editor)
* [Atto エディター - アイコン マッピング](https://docs.moodle.org/311/en/Atto_editor#:~:text=in%20the%20editor.-,Atto%20editor%20toolbar,-Atto%20Row%201)
<br>

</details>

<details>

<summary><b>Microsoft 統合を通してスケジュール設定された会議は、Outlook または Teams のカレンダーに表示されますか? 会議が表示される標準的なタイムラインは何ですか?</b></summary>

アプリを通じてスケジュールされた会議は、チャネル会議に類似した Outlook または Teams カレンダーには表示されません。 コース チャネルのすべてのメンバーは、組み込みのチャネル リンクから直接会議に出席できます。 詳細については、「[チャネル会議](https://www.knowledgewave.com/blog/benefits-of-channel-meetings-in-microsoft-teams)」を参照してください。

ただし、招待にアクセスし、会議の招待の **[必須]** または **[オプション]** フィールドに参加者名を手動で追加し、参加者のカレンダーにリモート会議を表示することはできます。 標準のタイムラインは、会議の作成時にユーザーが指定した日付が基準になります。 詳細については、「[Teams の制限事項と仕様](/microsoftteams/limits-specifications-teams)」を参照してください。

<br>

</details>

<details>

<summary><b>製品や他の問題に関するサポートを受けることができるサポート サイトはありますか?</b></summary>

製品とサービスの問題や開発者コミュニティのヘルプに関するサポートとヘルプについては、「[サポートとフィードバック](/microsoftteams/platform/feedback)」を参照してください。
