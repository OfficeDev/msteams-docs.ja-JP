---
title: 概要 - アプリ Teams発行プロセスの概要
description: パートナー センターにアプリを提出し、アプリをパートナー ストア (および AppSource) に発行Microsoft Teamsについて説明します。
ms.topic: overview
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: eaebde76a3d1f387ba16c9fdc77670144d22fa61
ms.sourcegitcommit: 40aade608ee21f5d7d813bd145bef5736dc647f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/17/2022
ms.locfileid: "62881652"
---
# <a name="publish-your-app-to-the-microsoft-teams-store"></a>アプリをアプリストアMicrosoft Teamsする

アプリをアプリ内のストアに直接配布Microsoft Teams世界中の何百万人ものユーザーにリーチできます。 アプリがストアでも機能している場合は、潜在的な顧客に即座にアクセスできます。

また、Teamsストアに発行されたアプリは[、Microsoft AppSource](https://appsource.microsoft.com) に自動的に一覧表示されます。これは、アプリとソリューションのMicrosoft 365マーケットプレースです。

## <a name="understand-the-publishing-process"></a>発行プロセスについて

アプリの準備が整ったと感じたら、アプリをアプリストアに表示するプロセスをTeamsできます。

> [!TIP]
> 提出前の手順を密接に実行すると、Microsoft がアプリの発行を承認する可能性が高い可能性があります。

:::row:::
   :::column span="":::
      
   :::column-end:::
   :::column span="3":::
      :::image type="content" source="../../../assets/images/submission/teams-app-store-publish-process.png" alt-text="Teamsストア発行プロセス" lightbox="../../../assets/images/submission/teams-app-store-publish-process.png":::
   :::column-end:::
   :::column span="":::
      
   :::column-end:::
:::row-end:::

1. [アプリがTeamsと](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)ストアの標準を満たTeams確認するには、ストアの検証ガイドラインを確認します。

1. [パートナー センターの開発者アカウントを作成します](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)。

1. [自動テストの実行](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)、テスト ノートのコンパイル、ストア登録情報の作成など、レビュー プロセスを迅速化するための重要なタスクを含む、ストア申請を準備します。

1. [パートナー センターからアプリ](/office/dev/store/add-in-submission-guide) を提出します。

1. 申請に失敗した場合は、Microsoft と直接作業して問題を解決し、 [アプリを再送信します](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md)。

## <a name="what-to-expect-after-you-submit-your-app"></a>アプリを提出した後に何を期待しますか?

* **機能とエクスペリエンスの詳細なテスト**

  アプリは検証者によって十分にレビューされ、 [Microsoft Commercial Marketplace](/legal/marketplace/certification-policies) 認定ポリシーに準拠し、機能とユーザー エクスペリエンスのテスト、使いやすさチェック、メタデータ チェックに重点を置きます。 アプリの検証は、デスクトップ、Web、およびモバイル クライアント全体で実行されます。

* **ガイド付きアプリは、コンシェルジュ サービスを通じて公開されます**

  アプリに問題が見られない場合は、アプリが承認され、アプリストアにTeamsされます。 問題がある場合は、エラーの詳細を含む自動検証レポートをパートナー センターから受信します。 アプリを Teams ストアに正常に発行し、このプロセスをガイドするために、検証チームは、次の情報を含む、カスタマイズされたメールをコンシェルジェ サービス [teamsubm@microsoft.com](mailto:teamsubm@microsoft.com) から送信します。

   * すべての問題の概要

   * ポリシー リンクと分類に関するエラーまたは問題の詳細: 

     * 必須の修正: これらの問題は、アプリの承認前に修正する必要があります。

     * 推奨される修正: これらの問題は、アプリのエクスペリエンスを向上させる推奨事項として、アプリの承認後に修正できます。

     * Blocker: これらの問題により、検証チームはアプリの機能をさらにテストできないので、検証を続行するには解決する必要があります。

     * クエリ: これらのクエリを共有して、アプリに関連する特定の質問に対する回答を取得できます。

   * 書き込み命令またはビデオ形式を使用して問題を再作成する手順。

   * ガイダンス ドキュメントへのリンクを使用して報告された問題を修正するための推奨事項。
 
  問題の一覧を確認した後、報告された問題を修正し、更新されたアプリ パッケージを電子メールで共有して、検証チームがアプリを完全に再検証します。 報告された問題に関連するクエリがある場合は、検証チームに問い [合](mailto:teamsubm@microsoft.com) teamsubm@microsoft.com。

  アプリで残りの問題や回帰の問題が発生した場合、検証チームは更新された検証レポートを共有します。 アプリにブロック機能がある場合は、ブロックが解決された後にアプリが検証された際に新しい問題が報告される場合があります。 検証チームは、修正プログラムの展開後にアプリで回帰の問題に気付いた場合もあります。 バグで構成されるアプリのすべての問題を閉じ、アプリストアへの発行を承認するには、いくつかの再申請がTeamsされます。

  報告された問題はすべて閉じ、最終的な申請がパートナー センターで行われた後、検証チームはアプリを承認して発行します。 アプリをアプリストアで使用するには、少なくとも 1 営業日Teamsします。

## <a name="tips-for-rapid-approval-to-publish-your-app"></a>ヒントを公開する迅速な承認を得る

* **設計フェーズ中**

  アプリの [ライフ サイクル](prepare/teams-store-validation-guidelines.md) (設計フェーズ) の早い段階でストアの検証ガイドラインを確認し、ストア要件に合わせアプリを構築してください。 これらのガイドラインに沿ってアプリをビルドすると、ストア ポリシーに準拠しない場合に、再作業が防止されます。

* **アプリの申請の前に**

  1. [事前にパートナー センター アカウントを](prepare/create-partner-center-dev-account.md) 作成してください。 パートナー センター アカウントで問題が発生した場合 [は、](prepare/create-partner-center-dev-account.md)サポート チケットを [作成します](/azure/marketplace/partner-center-portal/support)。

  1. ストアの [検証ガイドラインを再度確認](prepare/teams-store-validation-guidelines.md) して、アプリがストア要件と一直線に配置していることを確認します。 これにより、アプリで発生する問題の数が減り、アプリの承認に時間がかかっています。

  1. アプリのテストと再テスト:

     1. 開発者ポータルを使用してアプリ Teams[を検証し](https://dev.teams.microsoft.com/home)、パッケージ エラーを特定して修正します。

        :::image type="content" source="../../../assets/images/submission/teams-validation-developer-portal.png" alt-text="ストアの検証":::
 
     1. アプリがストア ポリシーに準拠しているか確認するために、アプリの申請前にアプリを完全に自己テストします。 アプリをサイドロードTeams、アプリのエンド to エンド のユーザー フローをテストします。 機能が期待通り動作し、リンクが壊れず、ユーザー エクスペリエンスがブロックされず、制限が明確に強調表示されます。

     1. デスクトップ、Web、モバイル クライアント間でアプリをテストします。 アプリがさまざまなフォーム ファクターに対応している必要があります。

  1. アプリ [を提出する前](/azure/active-directory/develop/publisher-verification-overview) に発行元の確認を完了します。 問題が発生した場合は、解決のための [サポート チケットを](/azure/marketplace/partner-center-portal/support) 作成できます。

  1. アプリの申請の準備を行う際は、チェックリストに [従](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/submission-checklist) い、申請パッケージの一部として次の詳細を含める必要があります。

      1. 完全に検証されたアプリ パッケージ。

      1. アプリの機能をテストするための管理者および管理者以外のユーザー資格情報 (アプリがプレミアム サブスクリプション モデルを提供している場合)。

      1. アプリの機能とサポートされているシナリオを詳しく説明するテスト手順。

      1. アプリの機能にアクセスするために追加の構成が必要な場合のセットアップ手順。 また、アプリで複雑な構成が必要な場合は、プロビジョニングされた[](/office/developer-program/microsoft-365-developer-program-get-started)デモ テナントに管理者アクセス権を提供して、検証者が構成手順を省略することもできます。

      1. アプリのデモ ビデオ録画キー ユーザー フローへのリンク。 これは強くお勧めします。

* **アプリ申請の投稿**

  * 検証レポートを確認した後、検証レポートに関連するクエリを含む電子メール スレッドに返信するか、報告された問題を解決するために追加のサポートが必要な場合。

  * アプリが承認するまで、報告された問題を解決するための十分な開発者帯域幅があることを確認します。

  * 今後の[テストのためにアプリ](/microsoftteams/platform/concepts/deploy-and-publish/appsource/resolve-submission-issues) パッケージを共有する前に、コンシェルジェ サービス teamsubm@microsoft.com [](mailto:teamsubm@microsoft.com) 報告された問題はすべて解決済みです。 これにより、アプリの検証に必要な反復回数が減り、アプリの承認に要する時間が短縮されます。
  
  * 検証プロセス中にアプリの機能を変更しないようにします。 これにより、新しい問題が検出され、アプリの承認にかかる時間が長くなる可能性があります。

## <a name="see-also"></a>関連項目

* [アプリ ストアMicrosoft 365発行する](/office/dev/store/)
* [アップロードアプリTeamsする](~/concepts/deploy-and-publish/apps-upload.md)
* [組織にTeamsアプリを発行する](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
* [ユーザーのオンボーディング エクスペリエンスを計画する](../../design/understand-use-cases.md#plan-the-onboarding-experience)
* [モバイルでのタブ アプリの配布](../../../tabs/design/tabs-mobile.md#distribution)
* [収益化されたアプリのテスト プレビュー](prepare/Test-preview-for-monetized-apps.md)
