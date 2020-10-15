---
title: 提出のチェックリスト
description: Microsoft Teams アプリを AppSource に公開する前に使用するチェックリスト
keywords: teams 発行ストア office 発行チェックリスト Teams Teams アプリアプリソースの検証
ms.openlocfilehash: 4bbf5adb8594db0f7163db610b192dd8aaec37fb
ms.sourcegitcommit: 25afe104d10c9a6a2849decf5ec1d08969d827c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "48465923"
---
# <a name="prepare-for-appsource-submission"></a>AppSource 提出の準備  

AppSource にリストされるようにするには、アプリが承認プロセスを経る必要があります。 これは Microsoft Teams グループによって提供される無料のサービスで、アプリが説明どおりに動作することを確認し、適切なメタデータをすべて含み、エンドユーザーにとって有益なコンテンツを提供します。 迅速な承認を得るために、アプリが以下の要件とガイドラインを満たしていることを確認してください。

* **Distribution メソッド:** アプリがストアプラットフォームで公開されているかどうかを確認します。 AppSource に発行せずにアプリを配布するため [のその他のオプション](../../overview.md) があります。
* **検証ポリシー:** アプリは、現在のすべての [Appsource 検証ポリシー](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams)に合格する必要があります。 提出する前に [検証ツール](#teams-app-validation-tool) に対してアプリをチェックしてください。 これらのポリシーは変更される可能性があることに注意してください。
* **アプリの詳細ページ:** アプリは、  [アプリの詳細ページチェックリスト](detail-page-checklist.md)と連携する必要があります。
* **ヒントとよく発生するケース:** リストされている [ヒントおよび頻繁に失敗するケース](frequently-failed-cases.md)  に、アプリの提出と承認の時間を向上させるために、さらに注意を払ってください。
* **アプリマニフェスト:** アプリのマニフェストをアプリの [マニフェストチェックリスト](app-manifest-checklist.md)に照らして確認します。
* **テストとデバッグ:** アプリを完全に [テストおよびデバッグ](../../../build-and-test/debug.md)していることを確認してください。
* **メモのテスト:**[検証のためのテストメモを](#test-notes-for-validation)含める
* **プライバシーポリシー:**[プライバシーポリシー、使用条件、サポート url の](#privacy-policy-terms-of-use-and-support-urls)ガイドラインに従っていることを確認します。

上記のすべての要件を完了したら、 [パートナーセンター](/office/dev/store/use-partner-center-to-submit-to-appsource)を使用してパッケージを appsource に提出します。

## <a name="teams-app-validation-tool"></a>Teams アプリ検証ツール

アプリ検証ツールは、 [アプリ検証](#teams-app-validator) ツールと [事前チェックリスト](#preliminary-checklist)で構成されています。 このツールは、 [Appsource](/office/dev/store/submit-to-appsource-via-partner-center) で使用されているものと同じテストケースをレプリケートして、アプリの送信を評価します。 したがって、承認のためにソリューションを AppSource に提出する前に、すべてのテストケースに合格することが重要です。このツールは Teams プラットフォーム内のいくつかの領域にあります。

> [!div class="checklist"]
>
> * [**アプリの検証のホームページ**](https://dev.teams.microsoft.com/appvalidation.html)
> * [**Teams Visual Studio Code toolkit**](/toolkit/visual-studio-code-overview.md)
> * [**App Studio**](/concepts/build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a>Teams アプリの検証

[ **検証** ] ページでは、appsource に提出する前にアプリパッケージを確認できます。 アプリパッケージをアップロードすると、検証ツールは、すべてのマニフェスト関連のテストケースに対してアプリをチェックします。 失敗した各テストの説明には、エラーを解決するためのドキュメントリンクが記載されています。

![検証ツール](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a>事前チェックリスト

自動化が困難なテストシナリオでは、最も一般的に失敗しているテストケースの7つの事前チェックリストがあります。

![事前チェックリスト](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a>プライバシーポリシー、使用条件、およびサポート Url

### <a name="privacy-policy"></a>プライバシーポリシー

プライバシーポリシーのガイドライン:

> [!div class="checklist"]
>
> * プライバシーポリシーは、アプリや、すべてのサービスの全体的なポリシーに固有のものにすることができます。
> * 汎用プライバシーポリシーを使用する場合は、「サービス」、「アプリケーション」、および「プラットフォーム」を参照して、自分の web サイトだけでなく、Teams アプリを含める必要があります。
> * ユーザーデータストレージ、ユーザーデータの保存、削除、およびセキュリティ制御の処理方法を指定する必要があります。
> * 連絡先情報を含める必要があります。
> * 壊れたリンク、ベータ版 Url、またはステージング Url を含めることはできません。

### <a name="terms-of-use"></a>利用規約

使用条件ステートメントは、アプリまたはアドインオファーリングに固有であり、適用される必要があります。

### <a name="support-urls"></a>サポート Url

アプリの問題については、サポート Url で認証やログイン資格情報を要求する必要はありません。

## <a name="test-notes-for-validation"></a>検証のためのテストメモ

以下を含めるようにしてください。

* 少なくとも2つのログイン資格情報、1人の管理者、および1つの非管理者を指定する必要があります。

* 確認のため、提供するアカウントには事前に十分なデータが事前に設定されている必要があります。

* エンタープライズアプリ、サブスクリプションが必要なアプリ、または Office 365 テナント/ドメインの依存関係があるアプリについては、アプリが事前に構成されていないドメインで3番目のアカウントを指定する必要があります。これにより、初回実行のユーザー環境を検証することができます。

* アプリにプレミアム/アップグレード機能がある場合は、その機能をテストするために必要なアクセス権を持つアカウントを提供する必要があります。

* テストメモは、SharePoint にアップロードすることを選択できます。 その場合は、ファイルへのパブリックリンクを提供してください。

* **アカウントをテスト**します。 アプリがバックエンドからライセンスアカウントまたは安全なライセンスのみを許可する場合は、テストアカウントが必要です。 また、アプリで許可されているチーム/グループのチャットスコープがある場合は、チームのグループ作業のシナリオを検証するために、同じテナント内の2つのテストアカウントが必要です。

* **統合手順**。 アプリを使用するためにテナント管理者が事前構成する必要がある場合は、この手順を実行するか、検証のために構成された管理者と管理者以外のアカウントを指定してください。 注: [Office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) サブスクリプションにサインアップできます。 これは90日間 *無料* で、開発アクティビティに使用している間は継続的に更新されます。

* **Teams のアプリ機能に関するメモ**: teams 内でアプリが提供するすべての機能の詳細を確認し、各機能をテストするための手順を実行します。

* **アプリの機能を示すビデオ (オプション)**: アプリの機能を完全に理解するために、製品のビデオ録画を提供することができます。
