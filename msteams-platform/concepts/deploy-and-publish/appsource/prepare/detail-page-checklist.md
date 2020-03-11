---
title: 高度なアプリの詳細ページを作成する
description: アプリの詳細ページに必要なものを説明します。
keywords: teams 発行ストアの office 発行ポリシー AppSource コンテンツ
ms.openlocfilehash: 741bc7b623e97b338c54c4dcfec5b1ca75201867
ms.sourcegitcommit: 2a84a3c8b10771e37ce51bf603a967633947a3e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2020
ms.locfileid: "42582868"
---
# <a name="build-a-great-app-details-page"></a>高度なアプリの詳細ページを作成する

[詳細] ページは、アプリの最初の印象です。 詳細ページの各要素を使用して、ビジョンとドライブのダウンロードを伝えることができます。アプリの表示を制限された領域で実現する方法を検討します。 アプリをインストールする前にユーザーを参加させるためのヒントと秘訣を次に示します。

> [!NOTE]
> アプリ[の情報が、有効なストアの一覧を作成するための Appsource ガイダンス](/office/dev/store/create-effective-office-store-listings)に従っていることを確認してください。

## <a name="app-name"></a>アプリ名

アプリの名前は、ユーザーが AppSource app store で検出する方法で重要な役割を果たします。 アプリの短縮名が [詳細] ページに表示されます。

**手順は次のとおりです。**

* アプリの動作についてヒントを示す、わかりやすいシンプルな名前を選びます。
* 特徴的です。

**注意事項**

* 既存のアプリ名と同じような汎用用語または名前を使用しないでください。
* アプリ名には、"Teams"、"Microsoft"、または "app" を使用しないでください。
![アプリケーション名ストアビュー](~/assets/images/store-detail-page/AppName-02.png)
![アプリ名 app Studio ビュー](~/assets/images/store-detail-page/AppName-01.png)

## <a name="color-icon"></a>色アイコン

これは、ユーザーによって最初に表示される要素の1つです。 これは、アプリストアをスクロールするときに魅力的で目立つものにする必要があります。 最初の印象を適切にし、ブランドの画像と目的を伝えることができるようにしてください。 AppSource には[、一貫性のあるビジュアル id を作成するため](/office/dev/store/create-effective-office-store-listings#create-a-consistent-visual-identity)のヒントが追加されています。

![アプリアイコンストアビュー](~/assets/images/store-detail-page/AppIcon-02.png)
![アプリのアイコンアプリ Studio ビュー](~/assets/images/store-detail-page/AppIcon-01.png)

## <a name="outline-icon"></a>アウトラインアイコン

これは、ユーザーおよび左側のナビゲーションメニューでお気に入りとしてマークされたメッセージング拡張機能で使用されます。 シンプルで認識可能であることを確認してください。 アウトラインアイコンには、白と透明度のみが含まれている必要があります (その他の色は使用できません)。 必要な仕様については、「 [Microsoft Teams アプリアイコン用のアプリパッケージを作成する](../../../build-and-test/apps-package.md#icons) *」を参照してください*。

![アプリアイコンアウトラインストア表示](~/assets/images/store-detail-page/AppIconOutline-02.png)
![アプリのアイコンアウトラインアプリ Studio ビュー](~/assets/images/store-detail-page/AppIconOutline-01.png)

## <a name="short-description"></a>簡潔な説明

これは、アプリの簡潔な概要です。 これは、対象ユーザーに直接伝わる独創性に満ちた魅力的なものにします。 理想的には、1つの文で、ソリューションとその価値をユーザーに説明します。

**手順は次のとおりです。**

* 最も重要な情報を最初に説明します。
* 顧客が検索する可能性があるキーワードを含めます。

**注意事項**

* タイトルを繰り返さないでください。
* 専門用語や専門用語を使用しないでください。ユーザーが検索対象を知っているとは想定できません。

![短い説明ストアビュー](~/assets/images/store-detail-page/ShortDescription-02.png)

[アプリ Studio](https://aka.ms/InstallTeamsAppStudio)のビューを次に示します。

![短い説明 App Studio ビュー](~/assets/images/store-detail-page/ShortDescription-01.png)

## <a name="long-description"></a>詳しい説明

これにより、ソリューションの主な機能、解決される問題、および対象ユーザーを強調することができます。 最初の文を使用して、アプリの固有の機能を伝えることによって、対象ユーザーに通知します。 説明は4000文字未満である必要があります。 多くのユーザーは、300と500の単語の間でのみ読み取りを行います。

>[!IMPORTANT]
> AppSource エントリで記述した説明をマニフェストに正確にコピーしてください。値は一致している必要があります。 Teams では、マニフェストで指定した説明のみが使用されます。

**手順は次のとおりです。**

* [Markdown の書式設定](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772)を使用して、説明を表示します。  
* 閲覧者が説明をスキャンするのに役立つ機能の一覧を示します。
* アクティブな音声を使用して、ユーザーに直接話します。
* 機能の一覧を表示するには、箇条書きを使用します。
* 質問がある場合にユーザーに連絡する方法がわかるように、ヘルプまたはサポートリンクを含めます。
* ユーザーガイダンスを改善するために、制限または制約を必ず呼び出してください。


>[!NOTE]
>Teams は、次の Markdown 構文をサポートしています。  
> **リンク**。 `[title](url/address/here)`.  
>**画像**。`![alt text](url/address/here)`.  
> **太字** `**bold text**`   `__bold text__`.  
> **斜体** `*italicized text*`  `_italicized text`.  
>**[順序付きリスト](https://www.markdownguide.org/basic-syntax/#ordered-lists)**<br>
>`1. first`  <br>` 1. second `  <br>`1.third`<br>
>**[順序なしリスト](https://www.markdownguide.org/basic-syntax/#unordered-lists)**<br>
` - short` <br>`- bulleted` <br>`- list`<br>
>**改行**。 `Place two empty spaces or a backslash \`  \
`at the end of a line.`<br>
 >**エスケープ.** 特殊文字をエスケープするには、インラインバックスラッシュを使用します。 `\*asterisk`.

**注意事項**

* 説明にはあまり多くのキーワードを含めないでください。これは煩雑であり、アプリの検出性に役立ちません。

![アプリの長い説明ストアビュー](~/assets/images/store-detail-page/LongDescription-02.png)

[アプリ Studio](https://aka.ms/InstallTeamsAppStudio)のビューを次に示します。

![アプリの長い説明 App Studio ビュー](~/assets/images/store-detail-page/LongDescription-01.png)

## <a name="screenshots"></a>スクリーンショット

[パートナーセンター](https://partner.microsoft.com)にアップロードされたスクリーンショットは、Teams クライアントの[appsource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)とアプリの一覧の両方に表示されます。 アプリの説明と共にアプリのビジュアルプレビューを提供します。
.Png、.jpg、.gif ファイルとして書式設定された1つのスクリーンショットを提供できます。 スクリーンショットは、最大サイズが 1024 KB で 1366 x 768 ピクセルでなければなりません。

**手順は次のとおりです。**

* アプリのすべての機能を強調表示することに重点を置いてください。
* コンテンツは、アプリを正確に表す必要があります。
* テキストは、過剰でない状態で適切に設定する必要があります。
* スクリーンショットを背景色で囲み、 [Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview)の例のようなマーケティングコンテンツを追加することができます。ただし、この寸法のスクリーンショットは表示されませんが、全体的な画像は含まれません。

<img width="800px" title="Freshdesk のスクリーンショット" src="~/assets/images/freshdesk.png" />

**注意事項**

* 電話機やラップトップなど、特定のデバイスを表示しません。
* アプリの外部から chrome/UI を表示しないようにします。
* スクリーンショットに Teams またはブラウザー UI をキャプチャしないでください。
* アプリを正確に反映しないモックを含めないでください。これには、Teams タブではなく web サイトを表示するなどの実際の UI が表示されます。

ベストプラクティスの詳細については、以下を*参照して*ください。 [appsource store の画像を有効](/office/dev/store/craft-effective-appsource-store-images)にします。

## <a name="videos"></a>ビデオ

画像が1000単語に値する場合、ビデオは1000個の画像になる価値があります。 ビデオは、アプリを使用する利点を伝える最も効果的な方法です。 [アプリの詳細] ページのすべてのスクリーンショットの前に配置されます。 アプリがどのように機能するか、どのようなことができるか、それを使用する利点、およびその作成者について説明してください。 プレゼンテーションは、わずか30-90 秒の間に短縮して、常にわかりやすいものにしてください。

## <a name="learn-more"></a>詳細情報

[アプリ送信用のチェックリスト](~/concepts/deploy-and-publish/appsource/publish.md)。  
[Microsoft Teams アプリ用のアプリパッケージを作成](~/concepts/build-and-test/apps-package.md)します。  
[パートナーセンターを使用して、ソリューションを AppSource に提出](/office/dev/store/use-partner-center-to-submit-to-appsource)します。
