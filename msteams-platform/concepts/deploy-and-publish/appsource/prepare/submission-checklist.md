---
title: ストア提出チェックリスト
description: Microsoft Teams アプリを AppSource に発行する前に使用するチェックリスト
ms.topic: reference
localization_priority: Normal
keywords: teams 発行ストア オフィス発行チェックリスト申請 Teams アプリ appsource 検証
ms.openlocfilehash: 1e7698e143d313ce46b834eada608571e3280b8a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020787"
---
# <a name="prepare-for-appsource-submission"></a>AppSource 申請の準備  

AppSource に一覧表示するには、アプリが承認プロセスを通過する必要があります。 これは、Microsoft Teams グループが提供する無料のサービスで、アプリが説明に従って動作し、適切なすべてのメタデータを含み、エンド ユーザーにとって価値のあるコンテンツを提供します。 迅速な承認を実現するために、アプリが次の要件とガイドラインを満たしていることを確認します。

* **配布方法:** アプリがストア プラットフォームでの公開を意図することを確認します。 AppSource [に発行](../../overview.md) せずにアプリを配布する他のオプションがあります。
* **検証ポリシー:** アプリは、申請の前に、 [現在のすべての AppSource 検証ポリシーを渡](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) す必要があります。 
  > [!NOTE] 
  > Appsource 検証ポリシーは変更される可能性があります。
* **モバイルの準備:** アプリはモバイル対応である必要があります。 アプリにタブが含まれている場合は、モバイル設計[](~/tabs/design/tabs-mobile.md)ガイドラインに従う必要があります。アプリはモバイル[](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment)OS (iOS と Android) でアップセルの要件を満たさなければならない必要があります。
* **アプリの自己テスト:** マニフェスト検証ツールを使用 [してアプリをテストします](#teams-app-validation-tool)。
* **アプリの詳細ページ:** アプリは、アプリの詳細ページチェックリスト  [と一致している必要があります](detail-page-checklist.md)。
* **ヒントと頻繁に失敗するケース:** アプリの申請と承認時間を改善するために、リストされている [ヒント](frequently-failed-cases.md)  と頻繁に失敗したケースに特に注意してください。
* **アプリ マニフェスト:** アプリ マニフェストのチェックリストに対して [アプリ マニフェストを確認します](app-manifest-checklist.md)。
* **テストとデバッグ:** アプリを完全にテストしてデバッグ [したと確認します](../../../build-and-test/debug.md)。
* **テストノート:** 検証用 [のテスト ノートを含める](#test-notes-for-validation)
* **プライバシー ポリシー:** プライバシー ポリシー [、使用条件](#privacy-policy-terms-of-use-and-support-urls) 、およびサポート URL がガイドラインに従う必要があります。

上記のすべての要件を完了したら、パートナー センターから AppSource にパッケージを [提出します](/office/dev/store/use-partner-center-to-submit-to-appsource)。

## <a name="teams-app-validation-tool"></a>Teams アプリ検証ツール

アプリ検証ツールは、アプリ検証ツール [と予備](#teams-app-validator) チェックリスト [で構成されます](#preliminary-checklist)。 このツールは [、AppSource](/office/dev/store/submit-to-appsource-via-partner-center) がアプリの申請を評価するために使用するのと同じテスト ケースをレプリケートします。 したがって、ソリューションを承認のために AppSource に提出する前に、すべてのテスト ケースに合格することが重要です。このツールは、Teams プラットフォーム内のいくつかの領域で確認できます。

> [!div class="checklist"]
>
> * [**アプリ検証機能のホームページ**](https://dev.teams.microsoft.com/appvalidation.html)
> * [**Teams Visual Studio コード ツールキット**](/toolkit/visual-studio-code-overview.md)
> * [**App Studio**](../../../build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a>Teams アプリ検証機能

[ **検証]** ページでは、AppSource に申請する前にアプリ パッケージを確認できます。 アプリ パッケージをアップロードするだけで、検証ツールはマニフェスト関連のすべてのテスト ケースに対してアプリをチェックします。 失敗したテストごとに、エラーの修正に役立つドキュメント リンクが説明されています。

![検証ツール](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a>予備チェックリスト

自動化が困難なテスト シナリオでは、予備チェックリストで最も一般的に失敗したテスト ケースの 7 つが表示されます。

![予備チェックリスト](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>プライバシー ポリシー、使用条件、サポート URL

### <a name="privacy-policy"></a>プライバシー ポリシー

プライバシー ポリシーのガイドライン:

> [!div class="checklist"]
>
> * プライバシー ポリシーは、アプリやすべてのサービスの全体的なポリシーに固有の場合があります。
> * 一般的なプライバシー ポリシーを使用する場合は、Teams アプリと Web サイトを含めるには、「サービス」、"アプリケーション"、および "プラットフォーム" を参照する必要があります。
> * ユーザー データストレージ、ユーザー データ保持、削除、およびセキュリティ制御の処理方法を含める必要があります。
> * 連絡先情報が含まれる必要があります。
> * リンクの破損、ベータ URL、ステージング URL は含めずにしてください。

### <a name="terms-of-use"></a>利用規約

使用条件ステートメントは、アプリやアドインの提供に固有で適用可能である必要があります。

### <a name="support-urls"></a>サポート URL

サポート URL では、アプリに関する問題について連絡するために、認証またはログイン資格情報を必要としない必要があります。

## <a name="test-notes-for-validation"></a>検証に関するテスト ノート

次の情報を含める必要があります。

* 少なくとも 2 つのログイン資格情報 、1 つの管理者と 1 つの管理者以外の資格情報を指定する必要があります。

* 検証の目的で、提供するアカウントには、十分な事前入力データが必要です。

* エンタープライズ アプリ、サブスクリプションが必要なアプリ、または Office 365 テナント/ドメイン依存関係があるアプリの場合は、最初に実行するユーザー エクスペリエンスを検証するために、アプリ用に事前構成されていない同じドメインに 3 番目のアカウントを提供する必要があります。

* アプリにプレミアム/アップグレードされた機能がある場合は、そのエクスペリエンスをテストするために必要なアクセス権を持つアカウントを提供する必要があります。

* テスト ノートを SharePoint にアップロードすることができます。 その場合は、ファイルへのパブリック リンクを指定してください。

* **テスト アカウント**. アプリでライセンスアカウントのみを許可するか、バックエンドからセーフリストに登録できる場合は、テスト アカウントが必要です。 また、アプリでチーム/グループ のチャット スコープが許可されている場合は、チーム の共同作業シナリオを検証するために、同じテナント内の 2 つのテスト アカウントが必要です。

* **統合手順**. テナント管理者による事前構成でアプリを使用する必要がある場合は、手順を含めるか、構成済みの管理者アカウントと管理者以外のアカウントを入力して検証します。 注: [365 Developer Program サブスクリプションOfficeサインアップ](https://developer.microsoft.com/microsoft-365/dev-program) できます。 これは 90 日間 *無料* で開発活動に使用する限り継続的に更新されます。

* **Teams のアプリ機能に関する注意事項**: Teams 内でアプリが提供する機能の詳細と、各機能のテスト手順について説明します。

* **アプリの機能を示すビデオ (オプション)**: 製品のビデオ録画を提供して、アプリの機能を完全に理解することができます。
