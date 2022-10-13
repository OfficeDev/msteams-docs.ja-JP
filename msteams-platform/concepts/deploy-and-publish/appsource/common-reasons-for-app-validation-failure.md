---
title: アプリ検証エラーの一般的な理由
description: リンクの破損、予期しないエラー、クラッシュ、有効なドメイン ガイドライン違反、機能バグなど、アプリ検証エラーの最も一般的な理由について説明します。
ms.topic: overview
author: v-ypalikila
ms.author: v-ypalikila
ms.localizationpriority: high
ms.openlocfilehash: 65144510fcb6a63c1c5cfaed4c344185917dee9a
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560653"
---
# <a name="common-reasons-for-app-validation-failure"></a>アプリ検証エラーの一般的な理由

ほとんどのアプリは、アプリの開発中に問題が発生したため、ストア申請プロセスに合格しません。 この記事の最も一般的な問題や理由については、[レビュー用の申請](/office/dev/store/add-in-submission-guide?toc=/microsoftteams/platform/toc.json&bc=/microsoftteams/platform/breadcrumb/toc.json)前にアプリを準備するのに役立ちます。 これらの一般的なエラーを回避し、[Microsoft Teams ストア検証ガイドライン](prepare/teams-store-validation-guidelines.md)と[コマーシャル マーケットプレース認定ポリシー](/legal/marketplace/certification-policies)に従うことで、アプリが Microsoft Teams ストア申請プロセスに合格する可能性を高めます。

アプリが拒否される最も一般的な理由は次のとおりです。

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/broken-links-errors-icon-1.png" link="#broken-links-functional-bugs-app-crashes-and-unexpected-errors":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/app-description-icon.png" link="#app-description":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/trademark-icon.png" link="#violation-of-microsoft-trademark-and-brand-guidelines":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/testability-icon.png" link="#testability":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/compliance-icon.png" link="#microsoft-365-app-compliance-program":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/app-guideline-icon.png" link="#violation-of-app-icon-guidelines":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/app-name-icon.png" link="#app-name":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/support-link-icon.png" link="#support-link":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/schema-icon.png" link="#manifest-schema":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/app-ui-icon.png" link="#app-ui":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column:::
      :::image type="icon" source="../../../assets/icons/domain-icon.png" link="#valid-domains":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/localization-icon.png" link="#localization-information":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../assets/icons/developer-name-icon.png" link="#provider-or-developer-name-mismatch":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/privacy-policy-icon.png" link="#privacy-policy":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../assets/icons/terms-of-use-icon.png" link="#terms-of-use":::
   :::column-end:::
:::row-end:::

## <a name="broken-links-functional-bugs-app-crashes-and-unexpected-errors"></a>リンクの破損、機能上のバグ、アプリのクラッシュ、予期しないエラー

アプリをテストして、アプリの正確性、機能、使用状況を確認します。 アプリを徹底的にテストし、アプリがサポートするすべてのエンド ツー エンド ワークフローを確認し、[コマーシャル マーケットプレース認定ポリシー](/legal/marketplace/certification-policies)に従ってオペレーティング システムとブラウザーでアプリの互換性をテストし、すべてのバグを修正します。 レビュー依頼を送信する前に、アプリで次の間違いを回避する必要があります。

* アプリ内のリンクが壊れています。

* アプリの使用をブロックする機能バグ。

* アプリがクラッシュします。

* アプリがサポートする記載されたワークフローを完了しないようにするアプリ サーフェイスの継続的な読み込み。

* アプリの使用、サインイン、サインアップ エクスペリエンス、およびアプリ機能が期待どおりに機能しないシナリオの間に予期しないエラー メッセージが表示されます。

* レビュー依頼を送信する前に、アプリが完了し、発行する準備が整っていることを確認します。

## <a name="app-description"></a>アプリの説明

優れた説明は、アプリを Microsoft Teams ストアで目立たせ、顧客にダウンロードを促すのに役立ちます。 アプリの説明で次の間違いを回避する必要があります。

* サインアップ、開始、ヘルプ、お問い合わせのリンクなど、新しいユーザーの情報を転送する方法は、マニフェストと AppSource の完全な説明には含まれません。

* リージョン固有のアプリ名または機能は、マニフェストとパートナー センター アプリの説明では呼び出されません。

* サインイン、サインアウト、サインアップ エクスペリエンスを完了するための外部アカウントまたはサービスに対する制限やアカウントの依存関係は、アプリ マニフェストや長い説明では呼び出されません。

* アプリ マニフェストの短い説明と完全な説明では、アプリの価値提案は強調表示されません。

* サポートされているアプリ機能は更新されません。

* 別のアプリとのアプリの比較。

* アプリ機能の一部ではない統合への参照。

* 文法エラー。

* アプリの短い説明と完全な説明は同じです。

## <a name="violation-of-microsoft-trademark-and-brand-guidelines"></a>Microsoft 商標およびブランド ガイドラインの違反

ロゴ、アイコン、デザイン、トレード ドレス、フォント、製品名、サービス、サウンド、絵文字、その他のブランド機能や要素を含む Microsoft のブランド資産は、登録または登録解除されたかのいずれかについて、Microsoft およびその会社のグループが所有する固有財産です。

Microsoft 商標、製品名、サービスを参照する場合は、[Microsoft 商標およびブランド ガイドライン](https://www.microsoft.com/legal/intellectualproperty/trademarks)に従う必要があります。 アプリの拒否につながる次の一般的な違反は回避する必要があります。

* プラン一覧で Microsoft を MS または MSFT と略し、プラン一覧の Microsoft Teams の最初のインスタンスを **Microsoft Teams** ではなく **Teams** として参照します。

* Microsoft からのエクスプレス ライセンスを使用することなく、プラン コンテンツで Microsoft ブランド資産を使用します。

* 偽装されたプランの一覧 (プランの説明、タイトル、アイコン、スクリーンショット、ビデオを含む) の作成、またはそれが Microsoft Teams ストアの公式 Microsoft アプリであるという印象操作。

## <a name="testability"></a>テスト可能性  

 [詳細なテスト手順](prepare/teams-store-validation-guidelines.md#app-package-and-store-listing)と資格情報は、アプリの正常なレビューに役立ちます。

パートナー センターの [証明書情報のメモ] セクションでアプリを確認するために必要なすべての詳細、サインインが必要な機能の有効なデモ資格情報、特別な構成を設定する手順、複製と完了が困難な環境を必要とする機能のデモ ビデオまたはハードウェアを指定してください。 また、最新の連絡先情報を入力してください。

アプリのレビュー中に拒否されたアプリの 20% で発生する次の問題を回避する必要があります。

* アプリをテストするためのテスト手順や資格情報はありません。

* コラボレーション シナリオをテストする 2 つのテスト アカウントとの依存関係がある場合に提供されるテスト アカウントは 1 つだけです。

* 提供されたテスト手順と資格情報は、アプリの機能テストを完了するのに十分ではありません。

## <a name="microsoft-365-app-compliance-program"></a>Microsoft 365 アプリ コンプライアンス プログラム  

Microsoft 365 アプリ コンプライアンス プログラムは、アプリに関するセキュリティおよびコンプライアンス情報を評価することにより、組織がリスクを評価し管理するのに役立ちます。 Microsoft Teams ストアで発行するレビューのためにアプリを送信する前に、[発行元の確認](/azure/active-directory/develop/mark-app-as-publisher-verified)を **完了する必要があります**。

## <a name="violation-of-app-icon-guidelines"></a>アプリ アイコン ガイドラインの違反

アイコンは、ユーザーが Microsoft Teams ストアを閲覧する際に目にする主要な要素の 1 つです。 アイコンは、アプリのブランドや目的を伝えるとともに、[アプリ アイコン ガイドライン](../../build-and-test/apps-package.md#app-icons)を満たす必要があります。 アプリの拒否につながる次の違反を回避する必要があります。

* 異なる色とアウトライン アイコン、または白と透明でないアウトライン アイコンに異なるアプリ パッケージが含まれるアプリの申請。

* パートナー センターのさまざまなロゴを含むアプリの申請と、レビュー用に送信されたアプリ パッケージ。

## <a name="app-name"></a>アプリ名

アプリ名は、ユーザーが Microsoft Teams ストアでアプリを検出するための重要な役割を果たします。 アプリ名が [アプリ名のガイドライン](prepare/teams-store-validation-guidelines.md#app-name)を満たし、[Microsoft 商標およびブランド ガイドライン](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks)に違反していないことを確認します。 アプリの拒否につながる次の違反を回避する必要があります。

* アプリの機能全体でのアプリ名の使用に一貫性がありません。
* アプリ パッケージとパートナー センターの一部として送信されたアプリ マニフェストに記載されているアプリ名が一致しません。
* *ベータ版*、*開発版*、*製品版* が追加されたアプリ名は、アプリの運用準備ができていないことを示します。
* 開発者がアプリ名を変更したものの、以前のアプリ名がアプリ内で引き続き使用されているアプリの申請。

## <a name="support-link"></a>サポート リンク

 サポート リンクは、ユーザーに認証を求めず、適切なサポート情報に直接誘導する必要があります。 ユーザーが連絡するための有効なサポート リンクがアプリにあることを確認する必要があります。

## <a name="manifest-schema"></a>マニフェスト スキーマ

Teams アプリ マニフェストは、アプリが Microsoft Teams 製品にどのように統合されるかを説明します。 アプリ マニフェストは、一般公開された[マニフェスト スキーマ](../../../resources/schema/manifest-schema.md)に適合している必要があります。 アプリでローカライズがサポートされている場合は、ローカライズ マニフェスト スキーマ バージョン 1.5 以降を使用してください。 プレビュー スキーマを含むアプリ パッケージ (パブリックにリリースされていない) は、アプリのレビューに失敗します。

アプリ更新プログラムを送信する場合は、マニフェストで宣言されているアプリ バージョンを更新する必要があります。 新しいアプリまたはアプリ更新プログラムを送信する場合は、常に最新の公開マニフェスト スキーマを使用し、Microsoft Teams ストアと Microsoft AppSource のマニフェスト スキーマのバージョンが同じであることを確認することをお勧めします。

アプリ パッケージには、アプリのマニフェスト、色アイコン、アウトライン アイコンのみが含まれている必要があります。 その他のファイルまたはフォルダーを含むアプリ パッケージは、アプリのレビューに失敗します。

## <a name="app-ui"></a>アプリ UI

アプリの UI は不完全に見えてはなりません。直感的である必要があります。 アプリの UI でアクションを実行する場合に、ユーザーに空白の画面が表示されないようにします。 コンテンツが切り捨てられているか重複しているアプリと、壊れた画像を表示するアプリは、アプリのレビューに失敗します。

## <a name="valid-domains"></a>有効なドメイン

アプリの申請は、Microsoft のコマーシャル マーケットプレース認定ポリシーに基づく[外部ドメイン](/legal/marketplace/certification-policies) ガイドラインに準拠している必要があります。 アプリがレビューに合格するには、アプリ マニフェストに一覧表示されている有効なドメインが組織の直接制御下にあることを確認します。

## <a name="localization-information"></a>ローカライズ情報

アプリでローカライズがサポートされている場合は、アプリ パッケージにローカライズされた言語ファイルを含める必要があります。 ローカリゼーション ファイルは、[Teams のローカリゼーション スキーマ](../../build-and-test/apps-localization.md)に準拠している必要があります。 ローカライズをサポートしているものの、アプリ マニフェストでローカライズ情報が見つからないアプリは、アプリのレビューに失敗します。

## <a name="provider-or-developer-name-mismatch"></a>プロバイダー名または開発者名の不一致

Microsoft Teams ストアまたは Microsoft AppSource からのアプリの取得中にエンド ユーザーが混乱しないように、両方のネットショップでプラン一覧に同じ開発者名を指定する必要があります。 開発者名が一致しないプランは、多くの場合、アプリのレビューに失敗します。

## <a name="privacy-policy"></a>プライバシー ポリシー

プラン一覧には、有効なプライバシー ポリシーのリンクを含める必要があります。 無効な、セキュリティで保護されていない、破損したプライバシー ポリシーのリンクを含むプランは、アプリのレビューに失敗します。 プライバシー ポリシーは、[プライバシー ポリシー ガイドライン](prepare/teams-store-validation-guidelines.md#privacy-policy)に従う必要があります。

## <a name="terms-of-use"></a>使用条件

プラン一覧には、有効な使用条件のリンクを含める必要があります。 無効な、セキュリティで保護されていない、破損した使用条件のリンクを含むプランは、アプリのレビューに失敗します。 [使用条件のガイドライン](prepare/teams-store-validation-guidelines.md#terms-of-use)に従う必要があります。

## <a name="see-also"></a>関連項目

* [Microsoft Teams ストア検証ガイドライン](prepare/teams-store-validation-guidelines.md)
* [商用マーケットプレース認定ポリシー](/legal/marketplace/certification-policies)
* [Microsoft 商標およびブランド ガイドライン](https://www.microsoft.com/legal/intellectualproperty/trademarks)
