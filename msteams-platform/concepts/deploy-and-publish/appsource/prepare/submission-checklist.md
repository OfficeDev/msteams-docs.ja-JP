---
title: 提出のチェックリスト
description: Microsoft Teams アプリを AppSource に公開する前に使用するチェックリスト
keywords: teams publish store office publishing checklist submission Teams apps appsource validation
ms.openlocfilehash: 8d20d0106c1b2d8da38c5802b977634925afffcc
ms.sourcegitcommit: db19fee033b41152267bb524d67aee5b7f64b04a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797476"
---
# <a name="prepare-for-appsource-submission"></a>AppSource 申請の準備  

AppSource に一覧表示するには、アプリが承認プロセスを実行する必要があります。 これは、Microsoft Teams グループによって提供される無料のサービスであり、アプリが説明されているとおりに動作し、適切なすべてのメタデータを含み、エンド ユーザーにとって有益なコンテンツを提供します。 迅速な承認を得る上で役立つには、アプリが次の要件とガイドラインを満たしていることを確認します。

* **配布方法:** アプリがストア プラットフォームで公開することを意図している必要があります。 AppSource [に公開](../../overview.md) せずにアプリを配布する他のオプションがあります。
* **検証ポリシー:** アプリは、申請前に現在のすべての [AppSource 検証ポリシーに合格](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) する必要があります。 
  > [!NOTE] 
  > Appsource 検証ポリシーは変更される可能性があります。
* **モバイルの準備:** アプリはモバイル対応である必要があります。 アプリにタブが含まれている場合は、モバイル設計[](~/tabs/design/tabs-mobile.md)ガイドラインに従う必要があります。また、アプリ[](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment)はモバイル OS (iOS および Android) のアップセル要件に準拠する必要はありません。
* **アプリの自己テスト:** マニフェスト検証ツールを使 [ってアプリをテストします](#teams-app-validation-tool)。
* **アプリの詳細ページ:** アプリは、アプリの詳細ページ  [のチェックリストと一致している必要があります](detail-page-checklist.md)。
* **ヒントとよく失敗するケース:** アプリの申請と承認時間を [改善するために、](frequently-failed-cases.md)  一覧表示されているヒントや頻繁に失敗するケースに特に注意を払います。
* **アプリ マニフェスト:** アプリ マニフェストのチェックリストに対して [アプリ マニフェストを確認します](app-manifest-checklist.md)。
* **テストとデバッグ:** アプリを完全にテストしてデバッグ [したと確認します](../../../build-and-test/debug.md)。
* **テストノート:** 検証用の [テスト ノートを含める](#test-notes-for-validation)
* **プライバシー ポリシー:** プライバシー ポリシー [、使用条件、](#privacy-policy-terms-of-use-and-support-urls) サポート URL がガイドラインに従って行う必要があります。

上記のすべての要件を完了したら、パートナー センターから AppSource にパッケージを [提出します](/office/dev/store/use-partner-center-to-submit-to-appsource)。

## <a name="teams-app-validation-tool"></a>Teams アプリ検証ツール

アプリ検証ツールは、アプリ検証ツール [と暫定的な](#teams-app-validator) チェックリスト [で構成されています](#preliminary-checklist)。 このツールは、アプリの申請を評価するために [AppSource](/office/dev/store/submit-to-appsource-via-partner-center) で使われるのと同じテスト ケースをレプリケートします。 したがって、ソリューションを承認のために AppSource に提出する前に、すべてのテスト ケースに合格することが重要です。このツールは、Teams プラットフォーム内のいくつかの領域で利用できます。

> [!div class="checklist"]
>
> * [**アプリ検証機能のホームページ**](https://dev.teams.microsoft.com/appvalidation.html)
> * [**Teams Visual Studio Code ツールキット**](/toolkit/visual-studio-code-overview.md)
> * [**App Studio**](/concepts/build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a>Teams アプリ検証機能

[ **検証]** ページでは、AppSource に提出する前にアプリ パッケージを確認できます。 アプリ パッケージをアップロードするだけで、検証ツールはマニフェストに関連するテスト ケースすべてについてアプリをチェックします。 失敗したテストごとに、エラーの修正に役立つドキュメント リンクが説明されています。

![検証ツール](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a>準備チェックリスト

自動化が困難なテスト シナリオの場合、暫定的なチェックリストには、最も一般的に失敗したテスト ケースの 7 つが示されています。

![準備チェックリスト](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>プライバシー ポリシー、使用条件、サポート URL

### <a name="privacy-policy"></a>プライバシー ポリシー

プライバシー ポリシーのガイドライン:

> [!div class="checklist"]
>
> * プライバシー ポリシーは、アプリやすべてのサービスの全体的なポリシーに固有のポリシーにできます。
> * 汎用のプライバシー ポリシーを使用する場合、Teams アプリと Web サイトを含めるには、"サービス"、"アプリケーション"、"プラットフォーム" を参照する必要があります。
> * ユーザー データの保存、ユーザー データの保持、削除、およびセキュリティ制御の処理方法を含める必要があります。
> * 連絡先情報を含める必要があります。
> * リンク切れ、ベータ版の URL、またはステージング URL を含めずにしてください。

### <a name="terms-of-use"></a>利用規約

使用条件に関する声明は、アプリやアドインの提供物に固有であり、適用される必要があります。

### <a name="support-urls"></a>サポート URL

サポート URL では、アプリに関する問題について連絡するために認証またはログイン資格情報を要求する必要があります。

## <a name="test-notes-for-validation"></a>検証のテスト ノート

以下を含める必要があります。

* 少なくとも 2 つのログイン資格情報 (1 人の管理者と 1 人の管理者以外) を入力する必要があります。

* 確認のために、提供するアカウントには、事前に入力された十分なデータが必要です。

* エンタープライズ アプリ、サブスクリプションが必要なアプリ、または Office 365 テナント/ドメインの依存関係があるアプリの場合は、初回実行時のユーザー エクスペリエンスを検証するために、アプリ用に事前に構成されていない同じドメイン内の 3 番目のアカウントを提供する必要があります。

* アプリにプレミアム/アップグレードされた機能がある場合は、そのエクスペリエンスをテストするために必要なアクセス権を持つアカウントを提供する必要があります。

* テスト ノートを SharePoint にアップロードすることができます。 その場合は、ファイルへのパブリック リンクを指定してください。

* **テスト アカウント**。 アプリでバックエンドからのライセンスアカウントまたはセーフリスト作成のみを許可する場合は、テスト アカウントが必要です。 また、アプリで許可されているチーム/グループ チャットスコープがある場合は、チームのコラボレーション シナリオを検証するために、同じテナント内に 2 つのテスト アカウントが必要です。

* **統合の手順**。 テナント管理者による事前構成でアプリを使用する必要がある場合は、手順を含めるか、構成済みの管理者アカウントと管理者以外のアカウントを入力して検証を行います。 注: Office [365 Developer Program サブスクリプションにサインアップ](https://developer.microsoft.com/microsoft-365/dev-program) できます。 これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。

* **Teams のアプリ機能** に関するメモ : Teams 内でアプリが提供する機能のすべてと、各機能をテストするための手順について詳しく説明します。

* **アプリの機能を** 示すビデオ (オプション) : 製品のビデオ録画を提供して、アプリの機能を完全に理解することができます。
