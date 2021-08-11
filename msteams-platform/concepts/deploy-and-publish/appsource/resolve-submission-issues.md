---
title: ストアの申請に関する問題を解決する
description: ストアの申請に関する問題のトラブルシューティングと修正Microsoft Teams理解します。
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: a18aff23b8523bc91485835c991cc6608deb8eae93ce175ff3403e699dc6c5e5
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705560"
---
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a>ストアの申請に失敗した場合Microsoft Teamsを解決する

Microsoft Teamsストアに発行されるアプリは、ストアのTeamsと[](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)商用マーケットプレース ポリシー[を満たす必要があります](/legal/marketplace/certification-policies)。

ストアの申請に失敗した場合、Microsoft は、アプリの準拠と公開に役立つコンシェルジュ検証サービスを提供します。

## <a name="get-help-directly-from-microsoft"></a>Microsoft から直接ヘルプを受ける

Microsoft が提供するコンシェルジュ検証サービスは、開発者がアプリをストアに公開Teamsします。 このサービスの一環として、Microsoft は、アプリが説明に従って動作し、適切なすべてのメタデータが含まれているか確認し、ユーザーに価値を提供します。

アプリの申請に失敗した場合、Microsoft は提出から 24 時間以内に推奨事項を含むレビュー レポートを送信します。

## <a name="resolve-issues-and-resubmit-your-app"></a>問題を解決し、アプリを再送信する

パートナー センターでアプリを再送信する前に、Microsoft のコンシェルジュ検証チームによって報告された問題を修正する必要があります。 Microsoft レポートには、次の情報が含まれています。

* 各問題 [に対応する検証](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) ガイドライン。
* 各問題を再現する方法について説明します。
* 一般に公開されている開発者向けドキュメントに基づいて各問題を解決するための推奨事項。

通常、問題を解決してアプリを再送信するプロセスは次のように行います。

1. レポート内のすべての問題を修正します。
1. 次の情報は、Microsoft のコンシェルジュ検証チーム <a href="mailto:teamsubm@microsoft.com">に送信</a>teamsubm@microsoft.com。
   * 更新されたアプリ パッケージ
   * アプリのテスト メモ (元の申請に含めなかった場合):
      * 少なくとも 2 つのアカウント (1 人の管理者と 1 人の管理者以外) の資格情報。
      * アプリを構成し、その機能をテストする手順。
      * アプリで使用されているアプリを示すビデオTeams。
1. Microsoft のコンシェルジュ検証チームは、更新されたアプリを完全にテストします。
1. 次のいずれかの操作を行います。
   * アプリに問題が発生する場合は、パートナー センターでアプリを再送信します。
   * 問題が解決しない場合、または Microsoft が新しい問題を見つけた場合は、修正する問題に関する別のレポートを受け取る必要があります。 これらの問題を解決し、更新されたバージョンのアプリをアプリに <a href="mailto:teamsubm@microsoft.com">送信</a>teamsubm@microsoft.com。

> [!CAUTION]
> 複数の申請に失敗しないようにするには、Microsoft のコンシェルジュ検証チームがアプリを承認するまで、パートナー センターでアプリを再送信しないようにしてください。

## <a name="faq"></a>よくあるご質問 (FAQ)

アプリの提出に関する問題を解決する際に、一般的な質問に対する回答を得る。

<br>

<details>

<summary><b>アプリの公開にどのくらいの時間が必要ですか?</b></summary>

ストアの申請に問題がない場合、アプリは 1 ~ 2 営業日以内に発行されます。 アプリが失敗した場合、Microsoft のチームが問題を解決するための推奨事項を提供します。 これらの修正を行い、更新されたアプリをそのチームに再送信すると、アプリを発行する準備ができているか、さらに作業が必要な場合は、24 時間以内に通知されます。

<br>

</details>

<details>

<summary><b>アプリが申請に合格する可能性を高める方法</b></summary>

次の手順を実行すると、申請が成功する可能性があります。

1. 設計ガイドラインに基づいて[Teamsを開発します](~/concepts/design/design-teams-app-overview.md)。
1. アプリがストア検証ガイドラインと Microsoft Teams[認定](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)ポリシーに準拠[している必要があります](/legal/marketplace/certification-policies)。
1. アプリ検証ツールを使用してアプリ Microsoft Teams[をテストします](https://dev.teams.microsoft.com/appvalidation.html)。
1. [ストアの申請Teams準備します](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)。

<br>

</details>

<details>

<summary><b>アプリはベータテスト中です。発行プロセスの時間を節約するためにアプリを提出できますか?</b></summary>

ちがいます。 Microsoft は、実稼働対応アプリのみを検証します。

<br>

</details>

<details>

<summary><b>パートナー センターで初めてアプリ teamsubm@microsoft.com する前に、メールの連絡先を確認できますか?</b></summary>

ちがいます。 Microsoft は、パートナー センターで初めてアプリを提出するまで、アプリの検証を開始しない。

<br>

</details>

<details>

<summary><b>パートナー センターから、アプリの発行が承認されたというメールが届いた。アプリがアプリストアにTeams理由</b></summary>

アプリが承認されると、発行には通常、アプリの機能に応じて 1 ~ 2 営業日かかる場合があります。2 営業日以内にアプリが公開されていない場合は、アプリに問い<a href="mailto:teamsubm@microsoft.com">合わせて teamsubm@microsoft.com。</a>

<br>

</details>
