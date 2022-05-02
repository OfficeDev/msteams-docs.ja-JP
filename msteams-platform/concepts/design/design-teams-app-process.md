---
title: アプリの設計プロセス
author: heath-hamilton
description: 効果的な Microsoft Teams アプリを設計するために、Microsoft のツールとリソースをいつどのように使用すればよいかについて概要を説明します。
ms.localizationpriority: high
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: b59c2c09240478899ff66e6554719f0f46bc791c
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111270"
---
# <a name="design-process-for-microsoft-teams-apps"></a>Microsoft Teams アプリの設計プロセス

Microsoft Teams アプリを設計するためのツールとリソースは複数あります。 次の手順では、設計プロセス中にこれらをいつどのように使用するかについて説明します。 (一部の手順は、技術的には設計プロセスの外部にある可能性がありますが、追加のコンテキストのために含まれています)。

:::image type="content" source="~/assets/images/design-guidelines/teams-app-design-process.png" alt-text="Teams アプリ設計プロセスの例を示す図。" border="false":::

## <a name="plan-your-app"></a>アプリを計画する

高品質の Teams アプリを設計するには、アプリで実現したいことと、ユーザーがそれをどのように使用するかを理解する必要があります。 ただし、設計を開始する前に次の質問に答えてみましょう。

* 対象ユーザーは誰か。
* 対象ユーザーの問題は何か。
* アプリでその問題を解決するにはどうすればよいか。
* アプリはどれくらいの頻度で使用されるか。
* アプリをどれほどのユーザーの数は使用するか。
* アプリでどのような投資収益率を提供できるか。

詳細については、[アプリのユース ケースの理解](~/concepts/design/understand-use-cases.md)、および [Teams へのユース ケースのマッピング](~/concepts/design/map-use-cases.md)に関する記事を参照してください。

## <a name="get-teams-design-tools"></a>Teams デザイン ツールを入手する

Microsoft は、Teams アプリの設計を容易にするツールを提供しています。 少なくとも、Microsoft Teams UI キットを使用することを強くお勧めします。

### <a name="get-the-microsoft-teams-ui-kit"></a>Microsoft Teams UI キットを入手する

Microsoft Teams UI キットは、効果的な Teams アプリを最短時間で開発するのに役立ちます。 この UI キットには、さまざまな例やバリエーションなど、Teams アプリの設計などに関連するこれらのドキュメントで目にするものがすべて含まれています。

この UI キットには、必要に応じてコピーおよび変更できる事前構築済みのテンプレートとコンポーネントも含まれています。そのため、ボタンをどんなデザインにすべきかなどを心配する代わりに、最適なユーザー エクスペリエンスの設計により多くの時間を費やすことができます。

> [!TIP]
> **この UI キットは自分にも関係があるだろうか?** Teams アプリの作成に関わっているなら、答えは "はい" です。 Teams アプリを作成する方法を理解することは、デザイナーだけでなく、プロダクト マネージャー、IDE を使用する開発者、ロー コード ツール (Microsoft Power Platform など) を使用してビルドしている開発者にも役立ちます。

1. [Microsoft Teams UI キット Figma ページ](https://www.figma.com/community/file/916836509871353159)に移動します。
1. **[Duplicate]\(複製\)** を選択して UI キットを開きます。 (最初に Figma アカウントを作成する必要がある場合があります)。

### <a name="try-the-sample-app"></a>サンプル アプリを試す

サンプル アプリをアップロードして、Teams クライアントでのアプリの外観と動作を確認できます。

> [!div class="nextstepaction"]
> [サンプル アプリを取得する (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="learn-teams-design-system"></a>Teams の設計システムを学習する

レイアウト、配色など、[Teams アプリの設計の基礎](design-teams-app-fundamentals.md)について詳しく読むか、少なくとも理解している必要があります。

## <a name="choose-app-capabilities"></a>アプリの機能を選択する

計画フェーズの後、アプリのユース ケースに適した Teams の機能を決定できます。 たとえば、ユーザーにプロアクティブに通知したい場合は、ボットが適切な機能である可能性があります。

この UI キットには、各機能が一般にはどのように追加、設定、使用、管理されているかを示す事前構築済みの設計が含まれています。 クイック リファレンスの情報はこれらのドキュメントにも含まれていますが、UI キットを使用すると、これらの設計の任意のものをアプリの設計にコピーして貼り付けることができます。

1. UI キットの左側のナビゲーションで、**[アプリの機能]** に移動し、アプリに必要な機能を選択します。
1. そのページから、アプリの設計に必要なものをコピーします。<br />
   たとえば、アプリでシングル サインオンによる認証をサポートする場合は、そのシナリオを処理するための設計をコピーして貼り付けます。

## <a name="design-your-ux-flow"></a>UX フローを設計する

基本的なアプリの設計が完了したら、UI キットから Teams の UI テンプレートと基本コンポーネントをコピーして、必要に応じて変更と調整を加えることができます。

### <a name="design-with-ui-templates"></a>UI テンプレートを使用したデザイン

UI テンプレートは、Teams の一般的なユース ケースとワークフローのための複雑で忠実度の高い設計です。 基本コンポーネントのレベルから始めるのではなく、これらのテンプレートを使用して設計プロセスの簡略化および時間短縮を図ることをお勧めします。

1. UI キットの左側のナビゲーションで、**[UI テンプレート]** に移動します。
1. アプリのデザインに適したテンプレートをコピーします。<br />
   たとえば、個人用アプリを設計する場合は、ダッシュボード テンプレートを使用できます。

### <a name="design-with-basic-ui-components"></a>基本 UI コンポーネントを使用した設計

Fluent UI に基づくこれらのコンポーネントは、使い慣れた Teams インターフェイスを作成するためのコア要素です。 UI テンプレートでは必要なものが不足している場合や、アプリを最初から設計したい場合は、これらのコンポーネントを使用します。

1. UI キットの左側のナビゲーションで、**[Basic UI components]\(基本 UI コンポーネント\)** に移動します。
1. アプリの設計に必要なコンポーネント (ボタンやトグルなど) をコピーします。

## <a name="implement-your-design"></a>設計を実装する

設計が完了し、ビルドを開始する準備が整いました。 次のツールは、アプリのフロントエンド開発を簡略化するのに役立ちます。

### <a name="build-with-ui-templates"></a>UI テンプレートを使用したビルド

設計で UI テンプレートを使用した場合は、Microsoft Teams UI ライブラリ (Fluent UI に基づく React コンポーネント ライブラリ) を使用してこれらのテンプレートを実装できます。

現時点では、UI キットにリストされているすべてのテンプレートがこのライブラリで使用できるわけではありません。

> [!div class="nextstepaction"]
> [ライブラリを入手 (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="build-with-basic-ui-components"></a>基本 UI コンポーネントを使用したビルド

デザイン フェーズとほぼ同じで、UI テンプレートでは必要なものが不足している場合や、アプリを最初からビルドしたい場合は、アプリ プロジェクトでこれらの Fluent UI コンポーネントを使用できます。 

(メモ: テンプレートでは不足がある場合やテンプレートのアイデアをお持ちの場合は、Teams UI ライブラリ リポジトリに貢献することをご検討ください)。

> [!div class="nextstepaction"]
> [ライブラリを入手 (Fluent UI)](https://fluentsite.z22.web.core.windows.net/)

## <a name="review-design-resources"></a>設計リソースを確認する

アプリの開発に着手したばかりの場合でも、実稼働可能なアプリの完成が間近な場合でも、次のリソースを定期的に確認することをお勧めします。

* **Microsoft Teams ストア検証ガイドライン**: ストアにリストされているアプリだけでなく、すべての Teams アプリが目指すべき標準を提供します。 詳細については、[ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)のページを参照してください。
* **設計のベスト プラクティス**: これらのドキュメントと UI キットは、高品質のアプリを設計するためのベスト プラクティスを提供します。 たとえば、[ボットを設計するためのベスト プラクティス](~/bots/design/bots.md#best-practices)に関する記事を参照してください。

## <a name="see-also"></a>関連項目

[アクティビティ フィード通知の設計](~/concepts/design/activity-feed-notifications.md)
