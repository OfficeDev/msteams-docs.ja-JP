---
title: 概要 - Microsoft Teams ストアにアプリを発行する
description: アプリをパートナー センターに送信し、Microsoft Teams ストア (および AppSource) に公開するためのプロセスについて説明します。
ms.topic: overview
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 248830328e68ce5c8e844a200501d240ff9e82ea
ms.sourcegitcommit: 1346b0eab13704807fca98f85c452214701d3fa2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2022
ms.locfileid: "64793798"
---
# <a name="publish-your-app-to-the-microsoft-teams-store"></a>Microsoft Teams ストアにアプリを発行する

アプリを Microsoft Teams 内のストアに直接配布して、世界中の何百万ものユーザーにリーチできます。 アプリがストアでも紹介されている場合は、潜在的な顧客に即座にリーチできます。

Teams ストアに公開されたアプリは、Microsoft 365 アプリおよびソリューションの公式マーケットプレイスである [Microsoft AppSource](https://appsource.microsoft.com) にも自動的に一覧表示されます。

## <a name="understand-the-publishing-process"></a>公開プロセスを理解する

アプリが運用環境に対応していると感じたら、Teams ストアにアプリを掲載するプロセスを開始できます。

> [!TIP]
> 送信前の手順に正確に従うと、Microsoft がアプリの公開を承認する可能性が高くなります。

:::row:::
   :::column span="":::

   :::column-end:::
   :::column span="3":::
      :::image type="content" source="../../../assets/images/submission/teams-app-store-publish-process.png" alt-text="Teams アプリ ストアの公開プロセス" lightbox="../../../assets/images/submission/teams-app-store-publish-process.png":::
   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

1. [Teams ストアの検証ガイドラインを確認して](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)、アプリが Teams アプリとストアの基準を満たしていることを確認します。

1. [パートナー センターの開発者アカウントを作成します](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)。

1. 自動テストの実行、テスト ノートの編集、ストア リストの作成など、レビュー プロセスを迅速化するための重要なタスクを含む、[ストア提出の準備をします](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)。

1. パートナー センターから[アプリを送信します](/office/dev/store/add-in-submission-guide)。

1. 送信に失敗した場合は、Microsoft と直接連携して[問題を解決し、アプリを再送信してください](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md)。

## <a name="what-to-expect-after-you-submit-your-app"></a>アプリを送信した後、何を期待しますか?

* **機能とエクスペリエンスの詳細なテスト**

  アプリは検証ツールによって徹底的にレビューされ、高度な機能とユーザー エクスペリエンスのテスト、使いやすさのチェック、メタデータチェックに重点を置いて、[Microsoft コマーシャルマーケットプレースの 認定ポリシー](/legal/marketplace/certification-policies)に準拠していることを確認します。アプリの検証は、デスクトップ、Web、およびモバイル クライアント間で実行されます。アプリの検証は、デスクトップ、Web、およびモバイル クライアント間で実行されます。

* **ガイド付きアプリはコンシェルジュ サービスを通じて公開します**

  アプリに問題がない場合、アプリは承認され、Teams ストアに公開されます。 問題がある場合は、パートナー センターから、障害の詳細が記載された自動検証レポートを受け取ります。 アプリを Teams ストアに正常に公開し、このプロセスをガイドするために、検証チームは、コンシェルジュ サービス [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) から次の情報を含むパーソナライズされたメールを送信します。

  * すべての問題のサマリー

  * ポリシー リンクと分類に関するエラーまたは問題の詳細:

    * 必須の修正: これらの問題は、アプリの承認前に修正する必要があります。

    * 推奨される修正: これらの問題は、アプリのエクスペリエンスを向上させるための推奨事項であるため、アプリの承認後に修正できます。

    * ブロッカー: これらの問題により、検証チームはアプリの機能をさらにテストできなくなり、検証を続行するには解決する必要があります。

    * クエリ: これらのクエリを共有して、アプリに関連する特定の質問への回答を得ることができます。

  * 書面による指示またはビデオ形式で問題を再現する手順。

  * ガイダンス ドキュメントへのリンクを使用して、報告された問題を修正するための推奨事項。

  問題のリストを確認したら、報告されたすべての問題を修正し、更新されたアプリ パッケージをメールで共有して、検証チームがアプリを徹底的に再検証できるようにします。 報告された問題に関連する質問がある場合は、検証チーム ([teamsubm@microsoft.com](mailto:teamsubm@microsoft.com)) に連絡してください。

  アプリに問題が残っているか、リグレッションの問題が観察された場合、検証チームは更新された検証レポートをあなたと共有します。 アプリにブロッカーが含まれている場合、ブロッカーが解決された後にアプリが検証されると、新しい問題が報告されることがあります。 検証チームは、修正の展開後のアプリのリグレッションの問題にも気付くことがあります。 バグで構成されるアプリのすべての問題をクローズし、Teams ストアへの公開が承認されるまでには、数回の再送信が必要です。

  報告されたすべての問題がクローズされ、パートナー センターで最終的な提出が行われた後、検証チームがアプリを承認して公開します。 アプリが Teams ストアで利用できるようになるまで少なくとも 1 営業日かかります。

* **アプリの使用状況を分析する**

  アプリが承認されて発行されたら、パートナー センターの [Teams アプリ使用状況レポート](/office/dev/store/teams-apps-usage) でアプリの使用状況を追跡できます。 メトリックには、月間、日単位、週単位のアクティブ ユーザー、リテンション期間と強度のグラフが含まれており、チャーンと使用量の頻度を追跡できます。

  新しく公開されたアプリのデータがレポートに表示されるまでに約 1 週間かかります。

## <a name="tips-for-rapid-approval-to-publish-your-app"></a>アプリを公開するための迅速な承認のヒント

* **設計フェーズ中**

  アプリのライフ サイクルの早い段階 (設計段階) で[ストア検証ガイドライン](prepare/teams-store-validation-guidelines.md)を確認し、ストアの要件に沿ってアプリを構築していることを確認します。 これらのガイドラインに沿ってアプリを構築すると、保存ポリシーに準拠していないためにやり直すのを防ぐことができます。

* **アプリの申請の前に**

  1. 事前に[パートナー センター アカウントを作成します](prepare/create-partner-center-dev-account.md)。 [パートナー センター アカウント](prepare/create-partner-center-dev-account.md)で問題が発生した場合は、[サポート チケット](/azure/marketplace/partner-center-portal/support)を作成します。

  1. [ストア検証ガイドライン](prepare/teams-store-validation-guidelines.md)を再度確認して、アプリがストア要件に適合していることを確認します。 これにより、アプリで観察される問題の数が減り、その結果、アプリの承認にかかる時間が短縮されます。

  1. アプリのテストと再テスト:

     1. Teams [開発者ポータル](https://dev.teams.microsoft.com/home)を使用してアプリ パッケージを検証し、パッケージ エラーを特定して修正します。

        :::image type="content" source="../../../assets/images/submission/teams-validation-developer-portal.png" alt-text="Teams ストア アプリの検証を開発者ポータル" lightbox="../../../assets/images/submission/teams-validation-developer-portal.png":::

     1. アプリを申請する前にアプリを徹底的にセルフテストして、ストア ポリシーに準拠していることを確認します。 Teams でアプリをサイドロードし、アプリのエンドツーエンドのユーザー フローをテストします。 機能が期待どおりに機能し、リンクが壊れていないこと、ユーザー エクスペリエンスがブロックされていないこと、制限事項が明確に強調されていることを確認してください。

     1. デスクトップ、Web、モバイル クライアント間でアプリをテストします。 アプリがさまざまなフォーム ファクターで応答することを確認します。

  1. アプリを送信する前に、[公開元の確認](/azure/active-directory/develop/publisher-verification-overview)を完了します。 問題が発生した場合は、解決のための[サポート チケット](/azure/marketplace/partner-center-portal/support)を作成できます。

  1. アプリの申請の準備をするときは、[チェックリストに従い](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/submission-checklist)、提出パッケージの一部として次の詳細を含めます。

      1. 徹底的に検証されたアプリ パッケージ。

      1. アプリの機能をテストするための管理者および非管理者のユーザー資格情報 (アプリがプレミアム サブスクリプション モデルを提供している場合)。

      1. アプリの機能とサポートされているシナリオの詳細を説明するテスト手順。

      1. アプリの機能にアクセスするために追加の構成が必要な場合のセットアップ手順。または、アプリで複雑な構成が必要な場合は、検証コントロールが構成手順をスキップできるように、管理者アクセス権を持つ [プロビジョニングされたデモ テナント](/office/developer-program/microsoft-365-developer-program-get-started) を提供することもできます。

      1. アプリのデモ ビデオ録画キー ユーザー フローへのリンク。強くお勧めします。

* **アプリの申請を投稿する**

  * 検証レポートを確認した後、検証レポートに関連する質問がある場合、または報告された問題を解決するために追加のサポートが必要な場合は、メール スレッドに返信してください。

  * アプリが承認されるまで、報告された問題を解決するのに十分な開発者帯域幅があることを確認してください。

  * さらにテストするためにアプリ パッケージを共有する前に、コンシェルジュ サービス [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) から報告された[すべての問題を解決した](/microsoftteams/platform/concepts/deploy-and-publish/appsource/resolve-submission-issues)ことを確認してください。 これにより、アプリの検証に必要な反復回数を減らし、その結果、アプリの承認にかかる時間を短縮できます。
  
  * 検証プロセス中にアプリの機能を変更しないようにします。これにより、新しい問題が検出され、アプリの承認にかかる時間が長くなる可能性があります。

## <a name="see-also"></a>関連項目

* [Microsoft 365 アプリ ストアへの公開](/office/dev/store/)
* [Teams アプリをアップロードする](~/concepts/deploy-and-publish/apps-upload.md)
* [Teams アプリを組織に公開する](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
* [ユーザーのオンボーディング エクスペリエンスを計画する](../../design/planning-checklist.md#plan-beyond-app-building)
* [モバイルでのタブ アプリの配布](../../../tabs/design/tabs-mobile.md#distribution)
* [収益化されたアプリのテスト プレビュー](prepare/Test-preview-for-monetized-apps.md)
* [Microsoft Teamsのランク付けパラメーター](post-publish/teams-store-ranking-parameters.md)
