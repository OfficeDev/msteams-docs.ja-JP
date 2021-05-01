---
title: アプリのストア登録情報を作成する
description: アプリのストア登録情報を作成するMicrosoft Teamsします。
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 270936ca967c17caaa8a56f85057b20ca3d6a409
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101430"
---
# <a name="create-a-store-listing-for-your-microsoft-teams-app"></a>アプリのストア登録情報をMicrosoft Teamsする

名前、説明、アイコン、[](https://partner.microsoft.com)画像&#8212;を含むパートナー センター&#8212;に送信する情報は、&#8212;アプリの Microsoft Teams ストアと Microsoft AppSource の一覧になります。

ストアの登録情報は、アプリの第一印象である可能性があります。 アプリの利点、機能、ブランドを効果的に伝えるリストを使用してインストールを増やします。

## <a name="specify-a-short-name"></a>短い名前を指定する

アプリの名前 (具体的には短い名前 [*)*](~/resources/schema/manifest-schema.md#name)は、ユーザーがストアでアプリを検出する方法において重要な役割を果たします。

次の例では、アプリの短い名前がストアの登録情報に表示される場所を強調表示します。

:::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="スクリーンショットの例は、アプリの短い名前がストアの登録情報に表示される場所を強調表示します。":::

### <a name="best-practices-for-names"></a>名前のベスト プラクティス

**するべきこと**

* アプリの動作をヒントにした、簡単で思い出に残る名前を選択します。
* 独特の特徴を持つ。
* 入力ミスや文法上のエラーを避ける。

**してはいけないこと**

* 不適切な用語または軽蔑的な用語を使用します。
* 人種的または文化的に無神経な言語を使用します。
* 既存のアプリに似た一般的な用語または名前を使用します。
* "Teams"、"Microsoft"、既存/今後の Microsoft 製品名、または "app" を名前に含める。

> [!NOTE]
> アプリが Microsoft との公式なパートナーシップの一部である場合は、アプリの名前が最初に指定されている必要があります (たとえば *、Salesforce Connector for microsoft* Microsoft Teams)。

## <a name="write-descriptions"></a>説明の書き込み

アプリの短い説明と長い説明が必要です。

### <a name="short-description"></a>簡潔な説明

対象ユーザーに対して、元の、魅力的で、指示する必要があるアプリの簡潔な概要。 理想的には、短い説明を 1 つの文にしてください。

次の例では、アプリの短い説明がストアの登録情報に表示される場所を強調表示します。

:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="スクリーンショットの例では、アプリの短い説明がストアの登録情報に表示される場所を強調表示します。":::

#### <a name="best-practices-for-short-descriptions"></a>短い説明のベスト プラクティス

**するべきこと**

* 最も重要な情報を最初に説明します。
* 顧客が検索する可能性が高いキーワードを含める。

**してはいけないこと**

* アプリ名を繰り返します。
* 専門用語や専門用語に頼る。 (ユーザーが何を探すのかを知っている場合は想定できない)。

### <a name="long-description"></a>詳しい説明

長い説明では、アプリの主な機能、解決する問題、ターゲットユーザーを強調する魅力的な説明を提供できます。 この説明は 4,000 文字までですが、ほとんどのユーザーは 300 ~ 500 語しか読み取りできません。

次の例では、アプリの長い説明がストア登録情報に表示される場所を強調表示します。

:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="スクリーンショットの例では、アプリの長い説明がストア登録情報に表示される場所を強調表示します。":::

#### <a name="usage-examples"></a>使用例

次の語句は、長い説明を書く際に許可される内容の例です。

* "<*アプリ名は、>* で動作Microsoft Teams"
* "..."<*アプリの>* のMicrosoft Teams"
* "<*アプリ名とアプリ名*> Microsoft Teams統合する"
* "...と統合Microsoft Teams"
* "...を使用するユーザー Microsoft Teams"
* "..."<*内の特定*>タスクMicrosoft Teams"
* "...に構築されています。."
* "...で実行されます。."
* "...によって有効になります。."
* ".....用に開発されました。
* "......" 用に設計されています。

#### <a name="best-practices-for-long-descriptions"></a>長い説明のベスト プラクティス

**するべきこと**

* Markdown [を使用して](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) 説明の書式を設定します。
* 説明を簡単にスキャンするために、箇条書きポイントを含む機能を一覧表示します。
* アクティブな音声を使用し、ユーザーに直接話します (たとえば *、..)。*
* ヘルプまたはサポート リンクを含める。
* 該当する場合は、制限、情報の設定、アカウントの依存関係、リリース更新プログラムを特定します。

**してはいけないこと**

* 500 単語を超える。
* キーワードが多すぎます。 (気を散らすので、アプリを見つけるのに役立つことはありません)。
* アプリが公式の認定プロセスを通過しない限り、次の言語を使用します。
  * "...の認定を受けています。
  * " ...によって動力を与えられた..."

### <a name="best-practices-for-all-descriptions"></a>すべての説明のベスト プラクティス

**するべきこと**

* 必要な場合にのみ、Microsoft 製品名を参照してください。 ガイドラインの詳細については、「Microsoft 商標とブランド [ガイドライン」を参照してください](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)。
* ファイルを参照する必要がある **場合Teams** 最初の参照を "Microsoft Teams"**とMicrosoft Teams。** 後続の参照は、次の参照に **短縮Teams。**
* 代わりに **Microsoft 365** を参照 **Office 365。**
* 入力ミスや文法上のエラーを避ける。
* 不要な大文字を避ける (たとえば、**ユーザー** ではなく **ユーザー)。**
* 頭字語は避ける。

**してはいけないこと**

* Microsoft を MS または **MSFT** と **略します**。
* Microsoft のスローガンやタグラインの使用を含め、アプリが Microsoft からのオファリングである場合を示します。
* 所有しない著作権で保護されたブランド名を使用します。

## <a name="adhere-to-icon-design-guidelines"></a>アイコンの設計ガイドラインに従う

アイコンは、ユーザーがストアを閲覧するときに表示される主な要素の 1 つです。 アイコンは、アプリのブランドの目的を伝える一方で、ユーザーの要件にTeamsがあります。

詳細については、「アプリ アイコン[の設計に関する具体的なTeams」を参照してください](~/concepts/build-and-test/apps-package.md#app-icons)。

## <a name="capture-screenshots"></a>スクリーンショットのキャプチャ

スクリーンショットは、アプリ名、アイコン、説明を補完するアプリの目立つ視覚的なプレビューを提供します。

### <a name="requirements-for-screenshots"></a>スクリーンショットの要件

* リストごとに最大 5 つのスクリーンショット。
* サポートされているファイルの種類には、PNG、JPEG、GIF が含まれます。
* ディメンションは 1366x768 ピクセルである必要があります。
* 最大サイズは 1,024 KB です。

### <a name="best-practices-for-screenshots"></a>スクリーンショットのベスト プラクティス

**するべきこと**

* アプリの機能 (ユーザーがボットと通信する方法など) に集中します。
* アプリを正確に表すコンテンツを含める。
* テキストを十分に使用します。
* 次の[Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview)の例と同様に、ブランドを反映し、マーケティング コンテンツを含む色のスクリーンショットをフレーム化します (ディメンション要件は、スクリーンショットではなく画像全体に適用されます):サードパーティアプリ:::image type="content" source="../../../../assets/images/freshdesk.png" alt-text="Freshdesk":::のスクリーンショットの例

**してはいけないこと**

* 電話やノート PC などの特定のデバイスを表示します。
* アプリに表示されていないクロムまたは UI を表示します。
* スクリーンショットにTeamsまたはブラウザーの UI をキャプチャします。
* アプリの実際の UI を不正確に反映するモックアップを含める (アプリをブラウザーで表示する場合は、[アプリ] タブではなくTeamsします。

ベスト プラクティスの詳細については [、「Microsoft アプリ ストアの効果的なイメージを作成する」を参照してください](/office/dev/store/craft-effective-appsource-store-images)。

## <a name="create-a-video"></a>ビデオを作成する

ビデオは、ユーザーがアプリを使用する理由を伝える最も効果的な方法です。 ビデオで次の質問に対処する必要があります。

* Whoアプリは何ですか?
* アプリで解決できる問題は何ですか?
* アプリの動作方法
* アプリを使用して得るその他の利点は何ですか?

ビデオを含める場合は、リストにスクリーンショットの前に表示されます。

### <a name="best-practices-for-videos"></a>ビデオのベスト プラクティス

* ビデオを 30 ~ 90 秒の間に保持します。
* 品質を目指します。 リストでは、スクリーンショットの前にユーザーにビデオが表示されます。

## <a name="localize-your-store-listing"></a>ストアの登録情報をローカライズする

パートナー センターは、 [ローカライズされたストアの登録情報をサポートしています](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions)。 詳細については、「アプリの登録[情報をローカライズするTeams」を参照してください](../../../../concepts/build-and-test/apps-localization.md)。

## <a name="see-also"></a>関連項目

* [効果的なストアMicrosoft 365を作成する](/office/dev/store/create-effective-office-store-listings)
* Teamsとコンテンツとブランドの表現に関[するアプリ設計](~/concepts/design/design-teams-app-fundamentals.md#copy-and-content)[ガイドライン](~/concepts/design/design-teams-app-fundamentals.md#brand-expression)
* [Microsoft 商標とブランド ガイドライン](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ストア申請の準備](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
