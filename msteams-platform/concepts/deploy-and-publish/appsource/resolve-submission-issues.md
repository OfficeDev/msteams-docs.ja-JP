---
title: ストアの申請に関する問題を解決する
description: Microsoft Teams ストアの申請に関する問題のトラブルシューティングと修正方法について説明します。 Microsoft から直接ヘルプを受け、問題を解決し、アプリを再送信します。
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: medium
ms.openlocfilehash: daa64a7f21071632b7c0728bf51829ca9540ebce
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100281"
---
# <a name="resolve-issues-if-your-teams-store-submission-fails"></a>Teams ストアの送信に失敗した場合に問題を解決する

Microsoft Teams ストアに発行されたアプリは、 [Teams ストアの検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) と [商用マーケットプレース ポリシー](/legal/marketplace/certification-policies)を満たしている必要があります。

ストアの申請が失敗した場合、Microsoft は、アプリの準拠と公開を支援するコンシェルジェ検証サービスを提供します。

## <a name="get-help-directly-from-microsoft"></a>Microsoft から直接ヘルプを受ける

Microsoft によって提供されるコンシェルジェ検証サービスは、開発者が Teams ストアにアプリを公開するのに役立ちます。 このサービスの一環として、Microsoft は、アプリが説明どおりに動作するかどうか、すべての適切なメタデータが含まれているかどうかを確認し、ユーザーに価値を提供します。

アプリの提出に失敗した場合、Microsoft は提出から 24 時間以内に推奨事項を含むレビュー レポートを送信します。

## <a name="resolve-issues-and-resubmit-your-app"></a>問題を解決し、アプリを再送信する

パートナー センターでアプリを再送信する前に、Microsoft コンシェルジェ検証チームによって報告されたすべての問題を修正する必要があります。 Microsoft レポートには、次の情報が含まれています。

* 各問題に対応する [検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) 。
* 各問題を再現する方法に関する手順。
* 公開されている開発者向けドキュメントに基づいて、各問題を解決するための推奨事項。

通常、問題を解決し、アプリを再送信するプロセスは次のようになります。

1. レポート内のすべての問題を修正します。
1. Microsoft コンシェルジェの検証チームに次の情報を <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a> に送信します。
   * 更新されたアプリ パッケージ
   * アプリのテスト ノート (元の申請にこれらを含めなかった場合):
      * 少なくとも 2 つのアカウント (管理者と管理者以外のアカウント) の資格情報。
      * アプリを構成し、その機能をテストする手順。
      * Teams で使用されているアプリを示すビデオ。
1. Microsoft コンシェルジェ検証チームは、更新されたアプリを完全にテストします。
1. 次のいずれかの操作を行います。
   * アプリに問題がなければ、パートナー センターにアプリを再送信します。
   * 問題が解決されない場合、または Microsoft が新しい問題を見つけた場合は、修正する内容に関する別のレポートが表示されます。 これらの問題を解決し、更新されたバージョンのアプリを <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a> に送信します。

> [!CAUTION]
> 複数の申請エラーを回避するには、Microsoft コンシェルジェ検証チームがアプリを承認するまで、パートナー センターでアプリを再送信しないでください。

## <a name="faq"></a>よく寄せられる質問

アプリの申請の問題を解決するときによく寄せられる質問に対する回答を取得します。

<br>

<details>

<summary><b>アプリを発行するのにどれくらいの時間がかかりますか?</b></summary>

ストアの申請に問題がない場合、アプリは 1 ~ 2 営業日以内に発行されます。 アプリが失敗した場合、Microsoft のチームから、問題を解決するための推奨事項が提供されます。 これらの修正を行い、更新されたアプリをそのチームに再送信すると、アプリを発行する準備ができているか、さらに作業が必要な場合は、24 時間以内に通知されます。

<br>

</details>

<details>

<summary><b>アプリ操作方法申請に合格する可能性を高めますか?</b></summary>

次の操作を実行すると、送信が成功する可能性があります。

1. [Teams の設計ガイドライン](~/concepts/design/design-teams-app-overview.md)に基づいてアプリを開発します。
1. アプリが [Teams ストアの検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) と [Microsoft コマーシャル マーケットプレース認定ポリシー](/legal/marketplace/certification-policies)に準拠していることを確認します。
1. [Microsoft Teams アプリ検証ツール](https://dev.teams.microsoft.com/appvalidation.html)を使用してアプリ パッケージをテストします。
1. [Teams ストアの申請を準備します](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)。

<br>

</details>

<details>

<summary><b>アプリがベータ テスト中です。発行プロセスの時間を節約するために、アプリを送信できますか?</b></summary>

いいえ。 Microsoft では、実稼働対応アプリのみが検証されます。

<br>

</details>

<details>

<summary><b>パートナー センターで初めてアプリを送信する前に、teamsubm@microsoft.com メールに問い合わせることはできますか?</b></summary>

いいえ。 パートナー センターで初めてアプリを送信するまで、Microsoft はアプリの検証を開始しません。

<br>

</details>

<details>

<summary><b>アプリの発行が承認されたことを示すメールがパートナー センターから届きました。Teams ストアにアプリがないのはなぜですか?</b></summary>

アプリが承認されると、発行には通常、アプリの機能に応じて 1 ~ 2 営業日かかります。アプリが 2 営業日後に発行されていない場合は、 <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a> にお問い合わせください。

<br>

</details>
