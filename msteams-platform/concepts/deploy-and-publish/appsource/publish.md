---
title: 概要 - Microsoft Teams ストアにアプリを公開する
description: アプリをパートナー センターに送信し、Microsoft Teams ストア (および AppSource) に公開するためのプロセスについて説明します。
ms.topic: overview
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: f8891edb11134570a79c5483eea722a44ad48b91
ms.sourcegitcommit: 377a4b712b50a211851aeecc1029414939945390
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2022
ms.locfileid: "68044652"
---
# <a name="publish-your-app-to-the-microsoft-teams-store"></a>Microsoft Teams ストアにアプリを公開する

アプリを Microsoft Teams 内のストアに直接配信して、世界中の何百万ものユーザーに届けることができます。 アプリがストアでも紹介されている場合は、潜在的な顧客に即座にリーチできます。

Teams ストアに公開されたアプリは、Microsoft 365 アプリおよびソリューションの公式マーケットプレイスである [Microsoft 商用マーケットプレイス](https://appsource.microsoft.com)にも自動的に一覧表示されます。

## <a name="understand-the-publishing-process"></a>公開プロセスを理解する

アプリが運用環境に対応している場合、Teams ストアにアプリを掲載するプロセスを開始できます。

> [!TIP]
> 提出前の手順に厳密に従うことで、Microsoft がアプリの公開を承認する可能性が高くなります。

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

1. レビュー プロセスの迅速化に役立つ重要なタスクは色々ありますが、特に自動テストの実行、テスト ノートの編集、ストア リストの作成などを行い、[ストアに提出する準備をします](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)。

1. パートナー センターから[アプリを送信します](/office/dev/store/add-in-submission-guide)。

1. 送信に失敗した場合は、Microsoft に直接連絡して[問題を解決し、アプリを再送信してください](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md)。

## <a name="what-to-expect-after-you-submit-your-app"></a>アプリを送信した後、何を期待しますか?

* **機能とエクスペリエンスの詳細なテスト**

  アプリは公開審査を行うチームによって徹底的にレビューされ、[Microsoft Commercial Marketplace の認定ポリシー](/legal/marketplace/certification-policies)に準拠していることを確認します。
  機能とユーザー エクスペリエンスの詳細なテスト、ユーザビリティ チェック、メタデータ チェックに焦点が当てられます。 アプリの検証は、デスクトップ、Web、およびモバイル クライアント間で実行されます。 提出後 24 時間以内に、詳細なテスト レポートを提供できるように努めています。

* **コンシェルジュ サービスによるアプリ公開の案内**

  アプリに問題がない場合、アプリは承認され、Teams ストアに公開されます。 一方、問題が存在する場合は、パートナー センターから、障害の詳細が記載された自動検証レポートを受け取ります。 アプリを Teams ストアにスムーズに公開できるように、またその一連の作業案内のために、審査チームはコンシェルジュ サービス [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) から個別に次の情報を含む電子メールで連絡を行います。

  * すべての問題のサマリー

  * ポリシー リンクと分類に関するエラーまたは問題の詳細:

    * 必須の修正: 問題は、アプリの承認前に修正する必要があります。

    * 推奨される修正: アプリのエクスペリエンスを向上させる推奨事項であるため、これらの問題はアプリの承認後に修正しても構いません。

    * ブロッカー: これらの問題により、審査チームはアプリの機能をこれ以上テストできないので、検証を続けるために解決する必要があります。

    * クエリ: クエリを共有して、アプリに関連する特定の質問への回答を得ることができます。

  * 書面による指示またはビデオ形式で問題を再現する手順。

  * ガイダンス ドキュメントへのリンクを使用して、報告された問題を修正するための推奨事項。

  問題のリストを確認したら、報告されたすべての問題を修正し、更新されたアプリ パッケージをメールで共有して、審査チームがアプリを徹底的に再検証できるようにします。 報告された問題に関連する質問がある場合は、審査チーム ([teamsubm@microsoft.com](mailto:teamsubm@microsoft.com)) に連絡してください。

  未解決の問題、リグレッションの問題がアプリに認められた場合、審査チームは更新された検証レポートをあなたと共有します。 アプリにブロッカーが含まれている場合、ブロッカーが解決された後にアプリが検証されると、新しい問題が報告されることがあります。 審査チームは、修正の展開後のアプリのリグレッションの問題にも気付くことがあります。 バグのあるアプリの問題をすべて解決し、Teams ストアへの公開の承認を得るには幾度か再送信が必要です。

  報告されたすべての問題がクローズされ、パートナー センターで最終的な提出が行われた後、検証チームがアプリを承認して公開します。 アプリが Teams ストアで利用できるようになるまで少なくとも 1 営業日かかります。

* **アプリの使用状況を分析する**

  アプリが承認されて発行されたら、パートナー センターの [Teams アプリ使用状況レポート](/office/dev/store/teams-apps-usage) でアプリの使用状況を追跡できます。 メトリックには、月間、日単位、週単位のアクティブ ユーザー、リテンション期間と強度のグラフが含まれており、チャーンと使用量の頻度を追跡できます。

  新しく公開されたアプリのデータがレポートに表示されるまでに約 1 週間かかります。

## <a name="tips-for-rapid-approval-to-publish-your-app"></a>迅速に承認を得てアプリを公開するヒント

* **設計フェーズ中**

  アプリのライフサイクルの早い段階 (設計段階) で[ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)を確認し、ストアの要件に沿ってアプリをビルドしていることを確認します。 ガイドラインに沿ってアプリをビルドすると、ストア ポリシー違反を理由に修正を余儀なくされることはなくなります。

* **アプリ提出の前に**

  1. 事前に余裕をもって[パートナー センター アカウントを作成します。](prepare/create-partner-center-dev-account.md) [パートナー センター アカウント](prepare/create-partner-center-dev-account.md)で問題が発生した場合は、[サポート チケット](/azure/marketplace/partner-center-portal/support)を作成します。

  1. [ストア検証ガイドライン](prepare/teams-store-validation-guidelines.md)を再度確認して、アプリがストア要件に適合していることを確認します。 レビューにより、アプリで観察される問題の数が減り、その結果、アプリの承認にかかる時間が短縮されます。

  1. アプリのテストと再テスト:

     1. Teams [開発者ポータル](https://dev.teams.microsoft.com/home)を使用してアプリ パッケージを検証し、パッケージ エラーを特定して修正します。

        :::image type="content" source="../../../assets/images/submission/teams-validation-developer-portal.png" alt-text="Teams ストア アプリの検証を開発者ポータル" lightbox="../../../assets/images/submission/teams-validation-developer-portal.png":::

     1. アプリを提出する前にアプリを徹底的にセルフテストして、ストア ポリシーに準拠していることを確認します。 Teams でアプリをサイドロードし、アプリのエンドツーエンドのユーザー フローをテストします。 機能が期待どおりに機能し、リンクが壊れていないこと、ユーザー エクスペリエンスがブロックされていないこと、制限事項が明確に強調されていることを確認してください。

     1. デスクトップ、Web、モバイル クライアント間でアプリをテストします。 アプリがさまざまなフォーム ファクターで応答することを確認します。
  
  1. アプリを送信する前に、[公開元の確認](/azure/active-directory/develop/publisher-verification-overview)を完了します。 問題が発生した場合は、解決のための[サポート チケット](/azure/marketplace/partner-center-portal/support)を作成できます。

  1. アプリ提出の準備をするときは、[チェックリストに従い](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/submission-checklist)、提出パッケージの一部として次の詳細を含めます。

        1. 徹底的に検証されたアプリ パッケージ。

        1. アプリの機能をテストするための管理者および非管理者のユーザー資格情報 (アプリがプレミアム サブスクリプション モデルを提供している場合)。

        1. アプリの機能とサポートされているシナリオの詳細を説明するテスト手順。

        1. アプリがアプリの機能にアクセスするために追加の構成が必要な場合のセットアップ手順。 または、アプリで複雑な構成が必要な場合は、[プロビジョニングされたデモ テナント](/office/developer-program/microsoft-365-developer-program-get-started)に管理者アクセスを提供して、公開審査を行うチームが構成手順をスキップできるようにすることもできます。

        1. アプリの主要なユーザー フローを示すデモ ビデオへのリンク。 これを強くお勧めします。

* **アプリ提出を投稿する**

  * 検証レポートを確認したら、検証レポートに関連するクエリを含む電子メール スレッドに返信するか、報告された問題を解決するために追加のサポートが必要な場合。

  * アプリが承認されるまで、報告された問題を解決するのに十分な開発者帯域幅があることを確認してください。

  * さらにテストするためにアプリ パッケージを共有する前に、コンシェルジュ サービス [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) から報告された[すべての問題を解決した](/microsoftteams/platform/concepts/deploy-and-publish/appsource/resolve-submission-issues)ことを確認してください。 これにより、アプリの検証に必要な反復回数を減らし、その結果、アプリの承認にかかる時間を短縮できます。
  
  * 検証プロセス中にアプリの機能を変更しないようにします。これにより、新しい問題が検出され、アプリの承認にかかる時間が長くなる可能性があります。

## <a name="additional-tips-for-rapid-approval-to-publish-your-app-linked-to-a-saas-offer"></a>SaaS オファーにリンクされたアプリを公開するための迅速な承認に関するその他のヒント

* **設計フェーズ中**

  [リンクされた SaaS オファーで公開されたアプリに固有のストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#apps-linked-to-saas-offer)をアプリのライフ サイクルの早い段階 (設計段階) で確認し、[SaaS オファーにリンクされた Teams アプリに適用されるストア要件と Microsoft Commercial Marketplace ポリシー](/legal/marketplace/certification-policies#11405-teams-app-linked-to-software-as-a-service-saas-offers)に沿ってアプリを構築するようにします。 ガイドラインに沿ってアプリをビルドすると、ストア ポリシー違反を理由に修正を余儀なくされることはなくなります。

* **アプリ提出の前に**

  1. アプリ提出の準備をするときは、次のことを確認してください。

      1. アプリは、AppSource のライブ (既に公開されている) SaaS オファーにリンクされており、価格情報を含む少なくとも 1 つのプランがあります。

      1. アプリ マニフェストに `publisherId.offerId` の形式で `subscriptionOffer` の詳細が正しく記載されています。

      1. リンクされた SaaS オファーが、 [SaaS 価格モデル](/azure/marketplace/create-new-saas-offer-plans)に割り当てられたライセンスをサポートするように設計されていることを確認する必要があります。

      1. テスト手順またはセットアップ手順を含めるか、アプリの機能とサポートされているシナリオの詳細を示すデモ ビデオへのリンク、およびテスターが SaaS ポータル ワークフローを簡単に理解できるようにするための追加情報を含めます。

  1. 検証のために SaaS オファーにリンクされたアプリを申請する前に、エンドツーエンドの購入およびライセンス管理ワークフローを徹底的に[セルフテスト](~/concepts/deploy-and-publish/appsource/prepare/test-preview-for-monetized-apps.md)する必要があります。次のことを確認してください。

     1. 管理者ユーザーと非管理者ユーザーの両方が注文を行い、サブスクリプションの購入を確認できます。 購入者は、Microsoft 管理センターで **[今すぐセットアップ]** を選択して、SaaS アプリケーションのランディング ページに移動できます。 購入者が SaaS アプリケーションでサブスクリプションをアクティブ化および構成できることをテストして確認します。 SaaS アプリケーションでのメッセージングは、購入者の道のりについて十分かつ明確な情報を提供する必要があります。

     1. Microsoft 管理センターの **[サブスクリプションの管理]** セクションには、テスト ユーザーによって提供されたサブスクリプションの正しい詳細が表示されます。 サブスクリプションの状態、ライセンスの数、およびその他の詳細は正確である必要があります。

     1. ライセンス ワークフローの購入と削除は期待どおりに機能しています。 購入者が Microsoft 管理センターからライセンスの数を増やすことができることを確認します。 SaaS アプリケーションのライセンス数と割り当てが、それぞれのライセンスと適切な担当者を反映していることを確認してください。 また、SaaS アプリケーションがユーザーからライセンスを取り除く方法を提供していることを確認してください。 ライセンスの削除後、残りの割り当てとカウントが SaaS アプリケーションにそのまま残り、正しい詳細が Microsoft 管理センターに反映されていることを確認します。

     1. サブスクリプションのキャンセルは期待どおりに機能しています。 購入者はサブスクリプションをキャンセルできます。 キャンセル後、正しいサブスクリプションの状態が Microsoft 管理センターと SaaS アプリケーションに反映されているかどうかを確認します。 キャンセルが成功した後、購入者がサブスクリプションにアクセスできなくなったことを確認します。

     1. サブスクリプションの再購入はシームレスです。 アクティブなサブスクリプションをキャンセルした後、購入者がサブスクリプションを再購入できることを確認するために徹底的にテストします。

     1. 購入者は、サブスクライブしたプランを変更できます。 プランが変更された後、ユーザーはアップグレードまたはダウングレードされたプラン機能にアクセスできます。

     1. SaaS アプリケーションには、ライセンス管理機能が含まれています。 購入者は、使用可能なライセンスをユーザーに割り当て、変更、および再割り当てできる必要があります。 購入者がライセンスを管理するためにユーザーを追加または削除できるかどうかを確認します。
  
  1. 最小ライセンス購入フローと一括ライセンス購入フローの両方が期待どおりに機能していることをテストして確認する必要があります。
  
  1. ライセンスが割り当てられているユーザーが、プランのリストに記載されている正確な購入済みプランの機能にアクセスできるようにする必要があります。

## <a name="see-also"></a>関連項目

* [Microsoft 365 アプリ ストアへの公開](/office/dev/store/)
* [Teams アプリをアップロードする](~/concepts/deploy-and-publish/apps-upload.md)
* [Teams アプリを組織に公開する](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
* [ユーザーのオンボーディング エクスペリエンスを計画する](../../design/planning-checklist.md#plan-beyond-app-building)
* [モバイルでのタブ アプリの配布](../../../tabs/design/tabs-mobile.md#distribution)
* [収益化されたアプリのテスト プレビュー](prepare/Test-preview-for-monetized-apps.md)
* [Microsoft Teamsのランク付けパラメーター](post-publish/teams-store-ranking-parameters.md)
