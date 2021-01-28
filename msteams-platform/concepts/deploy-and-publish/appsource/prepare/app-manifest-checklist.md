---
title: アプリ マニフェストのチェックリスト
description: Microsoft Teams アプリを AppSource に公開するためのアプリ マニフェストのチェックリスト
ms.topic: reference
keywords: teams publish store office publishing checklist
ms.openlocfilehash: f07c0d2693d12d56d6717724e1ef402cf79d5fff
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014398"
---
# <a name="app-manifest-checklist"></a>アプリ マニフェストのチェックリスト

>[!IMPORTANT]
>Office ソリューションの管理を販売者ダッシュボードからパートナー センターに移行しています。 詳細については、「[販売者ダッシュボードからパートナー センターへの移行](https://developer.microsoft.com/office/blogs/moving-management-of-solutions-from-seller-dashboard-to-partner-center/)」および「[よくあるご質問 (FAQ)](https://docs.microsoft.com/office/dev/store/partner-center-faq)」を参照してください。

アプリ マニフェストは、以下に示すガイドラインに従う必要があります。

>[!Tip]
> App Studio を使用して、アプリ マニフェストの構築を支援します。 以下のほとんどの要件が検証され、[テストと配布] タブにエラーまたは警告 **が表示** されます。

## <a name="tips"></a>ヒント

* アプリ名に "Teams"、"Microsoft"、"app" を使用しない。
* マニフェストの developerName は、パートナー センターで定義されているプロバイダー名と同じである必要があります。
* アプリの説明、スクリーンショット、テキスト、プロモーション用の画像がアプリのみを説明し、追加の広告、プロモーション、著作権で保護されたブランド名が含まれているのを確認します。
* 製品でサービスまたは別のサービスのアカウントが必要な場合は、説明に記載されているアカウントを一覧表示し、サインアップ、サインイン、サインアウトへのリンクが含めら確認します。
* 製品が正常に機能するために追加購入が必要な場合は、説明に記載します。
* マニフェストとパートナー センターまたはダッシュボードに、必要な使用条件とプライバシー ポリシーのリンクを提供します。 リンクが正しいドキュメント (理想的には Teams 固有) に正しく解決されていることを確認します。 ボットの場合は、Bot Framework 登録ページの [Submission] (提出) セクションで、同じ情報を入力する必要があります。
* マニフェスト内のメタデータがパートナー センター (および Bot Framework 登録のボットの場合) のメタデータと正確に一致する必要があります。 パートナー センターのエントリには、AppSource 製品ページで使用するために、より詳細で書式設定された説明が含まれている場合があります。
* マニフェストで使用されるアプリ タイトルが、パートナーセンターの申請で入力したアプリ タイトルと完全に一致する必要があります。 *「Microsoft* AppSource と Office で有効な登録情報を作成する [- 一貫性のあるアドイン名を使用する」を参照してください](https://docs.microsoft.com/office/dev/store/create-effective-office-store-listings#use-a-consistent-add-in-name)。

## <a name="metadata-requirement"></a>メタデータの要件

アプリには次のメタデータが必要です。

|データ|種類|Size|マニフェスト|パートナー センター|説明|
|---|---|---|---|---|---|
|アプリ パッケージ|.zip|||✔|アップロードまたは AppSource 申請用の実際のアプリ パッケージ。|
|カラー ロゴ|.png|192 &times; 192 ピクセル|`icon.color`||Teams ギャラリーの製品ページ一覧に表示するアイコン。 これがフルカラーの製品ロゴです。|
|ロゴアウトライン|.png|32 &times; 32 ピクセル|`icon.outline`||Teams、Teams チャット チャネル、その他の場所に表示するアイコン。 これは、背景が透明な白いアウトラインとしてレンダリングされるロゴです。|
|アプリ ロゴ|.png、.jpg、.jpeg、.gif|300 &times; 300 ピクセル||✔|AppSource に表示するアイコン。 これはフルカラーの製品ロゴであり、マニフェストで使用されるファイルとは異なるファイルです `icon.color` 。 512 KB 未満である必要があります。|
|サポート リンク|URL|||✔|アプリをインストールしていないエンド ユーザー向け資料をサポートするリンク。 ログイン (HTTPS) なしでアクセス可能な一般公開リンク。|
|プライバシー リンク|URL||`developer.privacyUrl`|✔|プライバシー ポリシー (HTTPS) へのリンク。|
|ビデオ リンク|URL|||オプション|アプリに関するビデオへのリンク。|
|EULA|.doc、.pdf など|||オプション|AppSource には、添付ファイルとして提供できるエンドユーザー ライセンス契約 (EULA) が必要です。 EULA を提出しない場合は、お客様に代わって EULA が提供されます。|
|サービス条件|URL||`developer.termsOfServiceUrl`||サービス利用規約 (HTTPS) へのリンク。|
|テスト ノート|インラインまたはパブリック URL へのリンクを入力する|||アプリケーションをステップ バイ ステップでテストする方法に関する詳細なテスト ノート。 管理者と管理者以外のシナリオをテストするには、2 つのログイン資格情報を含める必要があります。|

## <a name="localized-content"></a>ローカライズされたコンテンツ

> [!NOTE]
> AppSource は、次のメタデータのローカライズされたコンテンツをサポートする予定です。 現在、アプリの登録情報は AppSource では英語でのみ表示されますが、Teams クライアントでは適切にローカライズされた形式で表示されます。 詳 [しくは、アプリのローカライズ](~/concepts/build-and-test/apps-localization.md) に関するページをご覧ください。

|データ|種類|Size|マニフェスト|パートナー センター|説明|
|---|---|---|---|---|---|
|アプリ名|String|30|`name.short`|✔|ストアフロントと製品に表示されるアプリケーションの名前。|
|長いアプリ名|String|30|`name.full`|✔|ストアフロントと製品に表示されるアプリケーションの名前。|
|簡潔な説明|String|80|`description.short`|✔|アプリの簡単な説明。|
|詳しい説明|String|4000|`description.full`|✔|アプリの詳しい説明。 マニフェスト ファイルでは、正確な概要で十分です。 パートナー センターでは、AppSource 製品ページのより充実した形式の説明を使用できます。|
|スクリーン ショット (1 ~ 5)|.png、.jpg、または .gif|1366w x 768h、1024 KB より小さい||✔|アプリのエクスペリエンスを示す少なくとも 1 つのスクリーン ショット。 アプリの詳細ページで使用します。|

## <a name="submission-extras-for-bots"></a>ボットの追加提出

Microsoft Teams のボットは、Bot Framework を使用して作成する必要があります。 手順 [については、「ボットを作成する](~/bots/how-to/create-a-bot-for-teams.md) 」を参照してください。 Bot Framework でボットのアイコンに 96x96 カラー アイコンを使用します。
