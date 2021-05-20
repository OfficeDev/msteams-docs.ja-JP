---
title: ストアの提出に関する問題を解決する
description: Microsoft Teams ストアの提出に関する問題のトラブルシューティングと修正方法を理解する。
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 23c751d7a9fec96de128521f660213a559534283
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565110"
---
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a>Microsoft Teams ストアの送信に失敗した場合の問題の解決

Microsoft Teams ストアに公開されるアプリは、[ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)と[商用マーケットプレース ポリシー](/legal/marketplace/certification-policies)Teams を満たす必要があります。

ストアの提出に失敗した場合、Microsoft はアプリの準拠と公開を支援するコンシェルジュ検証サービスを提供します。

## <a name="get-help-directly-from-microsoft"></a>マイクロソフトから直接ヘルプを取得する

Microsoft が提供するコンシェルジュ検証サービスは、開発者がアプリをTeams ストアに公開するのに役立ちます。 Microsoft は、このサービスの一環として、アプリが説明どおりに動作し、すべての適切なメタデータを含み、ユーザーに価値を提供するかどうかを確認します。

アプリの提出に失敗した場合、Microsoft は提出から 24 時間以内に推奨事項を含むレビュー レポートを送信します。

## <a name="resolve-issues-and-resubmit-your-app"></a>問題を解決してアプリを再提出する

パートナー センターでアプリを再送信する前に、Microsoft コンシェルジュ検証チームによって報告されたすべての問題を修正する必要があります。 マイクロソフトのレポートには、次の情報が含まれています。

* 各問題に対応する [検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) 。
* 各問題の再現方法について説明します。
* 一般に公開されている開発者ドキュメントに基づいて、各問題を解決するための推奨事項。

問題を解決し、アプリを再送信するプロセスは、通常、次のようになります。

1. レポート内のすべての問題を修正します。
1. 次の情報は、teamsubm@microsoft.com の Microsoft コンシェルジュ検証 <a href="mailto:teamsubm@microsoft.com">チームに送信</a>します。
   * 更新されたアプリ パッケージ
   * アプリのノートをテストする (元の申請にメモを含めなかった場合):
      * 少なくとも 2 つのアカウントの資格情報 (1 人の管理者と 1 人の管理者以外)。
      * アプリを構成し、その機能をテストする手順。
      * Teamsで使用したアプリを示すビデオ。
1. Microsoft コンシェルジュ検証チームは、更新されたアプリを完全にテストします。
1. 次のいずれかの操作を行います。
   * アプリに問題が発生する場合は、パートナー センターでアプリを再送信します。
   * 問題が解決しない場合や、Microsoft が新しい問題を発見した場合は、修正の内容に関する別のレポートが表示されます。 これらの問題を解決し、アプリの更新版を <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>に送信します。

> [!CAUTION]
> 複数の送信エラーを回避するには、Microsoft コンシェルジュ検証チームがアプリを承認するまで、パートナー センターでアプリを再送信しないでください。

## <a name="faq"></a>FAQ

アプリの送信に関する問題を解決する際に、よく寄せられる質問に対する回答を得ることができます。

<br>

<details>

<summary><b>アプリの公開にはどのくらいの時間がかかりますか?</b></summary>

ストアの提出に問題がない場合、アプリは 1 ~ 2 営業日以内に公開されます。 アプリが失敗した場合、Microsoft のチームが問題を解決するための推奨事項を提供します。 これらの修正を行い、更新されたアプリをそのチームに再送信すると、アプリを公開する準備ができているか、さらに作業が必要な場合は、24 時間以内に通知されます。

<br>

</details>

<details>

<summary><b>アプリが申請に合格する可能性を高めるにはどうすればよいですか?</b></summary>

次の操作を行うと、送信が成功する可能性があります。

1. [Teams設計ガイドライン](~/concepts/design/design-teams-app-overview.md)に基づいてアプリを開発する 。
1. アプリが[Teamsストア検証ガイドラインと](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) [Microsoft 商用市場認定ポリシー](/legal/marketplace/certification-policies)に準拠していることを確認します。
1. [アプリの検証ツールを使用してアプリ パッケージをテストMicrosoft Teams。](https://dev.teams.microsoft.com/appvalidation.html)
1. [Teams ストアの提出を準備する](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md):

<br>

</details>

<details>

<summary><b>私のアプリはベータテスト中です。アプリを提出して、公開プロセスの時間を節約できますか?</b></summary>

いいえ。 マイクロソフトは、運用可能なアプリのみを検証します。

<br>

</details>

<details>

<summary><b>パートナー センターで初めてアプリを提出する前に、teamsubm@microsoft.com メールに連絡できますか?</b></summary>

いいえ。 マイクロソフトでは、パートナー センターで初めてアプリを提出するまで、アプリの検証を開始しません。

<br>

</details>

<details>

<summary><b>パートナー センターから、アプリの公開が承認されたというメールを受け取りました。アプリがTeams ストアにないのはなぜですか?</b></summary>

アプリが承認されると、通常、アプリの機能に応じて 1 ~ 2 営業日かかります。アプリが 2 営業日を過ぎるとアプリが公開されていない場合は <a href="mailto:teamsubm@microsoft.com">、teamsubm@microsoft.com</a>に連絡してください。

<br>

</details>
