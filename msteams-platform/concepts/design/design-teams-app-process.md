---
title: アプリの設計プロセス
author: heath-hamilton
description: Microsoft ツールとリソースを使用して効果的なアプリを設計する方法とMicrosoft Teams取得します。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 225859da18cb50741ab49c68d89bc318c6c9034c
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994211"
---
# <a name="design-process-for-microsoft-teams-apps"></a>アプリの設計プロセスMicrosoft Teamsする

アプリを設計するための複数のツールとMicrosoft Teamsがあります。 次の手順では、設計プロセス中にこれらをいつどのように使用できるのかについて説明します。 (一部の手順は技術的には設計プロセスの外にある場合がありますが、追加のコンテキストに含まれています)。

:::image type="content" source="~/assets/images/design-guidelines/teams-app-design-process.png" alt-text="アプリ設計プロセスのTeamsを示す図。" border="false":::

## <a name="plan-your-app"></a>アプリを計画する

高品質のアプリを設計Teamsするには、アプリで実行する操作と、ユーザーがアプリを使用すると思う方法を理解する必要があります。 ただし、設計を開始する前に、次の質問に答えます。

* 対象ユーザーは誰か。
* 彼らの問題は何ですか?
* アプリで問題を解決する方法
* アプリはどのくらいの頻度で使用されますか?
* アプリを使用するユーザーの数
* アプリが提供できる投資に対するリターンの種類は何ですか?

詳細については、「アプリの[使用例](~/concepts/design/understand-use-cases.md)を理解し、使用例をアプリにマップする」[を参照Teams。](~/concepts/design/map-use-cases.md)

## <a name="get-teams-design-tools"></a>設計Teams取得する

Microsoft では、アプリの設計を容易にするツールTeams提供しています。 少なくとも、UI キットを使用することを強Microsoft Teams推奨します。

### <a name="get-the-microsoft-teams-ui-kit"></a>UI キットMicrosoft Teams取得する

UI キットMicrosoft Teamsを使用すると、短時間で効果的Teamsアプリを開発できます。 UI キットには、アプリの設計に関連するこれらのドキュメントTeams、広範な例やバリエーションなど、すべて含まれています。

UI キットには、必要に応じてコピーや変更が可能なテンプレートとコンポーネントも用意されています。そのため、ボタンの外観を気にする代わりに、最適なユーザー エクスペリエンスの設計に多くの時間を費やできます。

> [!TIP]
> **UI キットは私用ですか?** アプリの作成に何か部分がある場合Teamsはい。 Teams アプリを作成する方法を理解すると、デザイナーだけでなく、製品管理者、IDEs を使用する開発者、および低コード ツール (Microsoft Power プラットフォームなど) を使用して構築するメーカーに役立ちます。

1. [UI キット[Figma] Microsoft Teamsページに移動します](https://www.figma.com/community/file/916836509871353159)。
1. [ **複製] を** 選択して UI キットを開きます。 (最初に Figma アカウントを作成する必要がある場合があります)。

### <a name="try-the-sample-app"></a>サンプル アプリを試す

サンプル アプリをアップロードして、アプリの外観と動作をクライアントで確認Teamsできます。

> [!div class="nextstepaction"]
> [サンプル アプリを取得する (GitHub)](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="learn-teams-design-system"></a>設計Teamsを学ぶ

レイアウト、配色など、Teamsアプリ[設計](design-teams-app-fundamentals.md)の基本について詳しい情報を読むか、少なくとも理解してください。

## <a name="choose-app-capabilities"></a>アプリの機能を選択する

計画フェーズの後で、アプリの使用Teams合う機能を特定できます。 たとえば、事前にユーザーに通知する場合、ボットが適切な機能である可能性があります。

UI キットには、ユーザーが通常、各機能を追加、設定、使用、管理する方法を示す、事前に構築されたデザインがあります。 この情報は簡単に参照できますが、UI キットを使用すると、これらのデザインをコピーしてアプリのデザインに貼り付けることができます。

1. UI キットの左側のナビゲーションで、[アプリの機能] に **移動し** 、アプリに必要な機能を選択します。
1. そのページから必要なデータをコピーして、アプリを設計します。<br />
   たとえば、アプリがシングル サインオンでの認証をサポートしている場合は、その正確なシナリオを処理するデザインをコピーして貼り付けます。

## <a name="design-your-ux-flow"></a>UX フローを設計する

基本的なアプリ設計が完了したら、UI キットから UI テンプレートと基本的なTeamsをコピーして、必要なだけ変更および調整できます。

### <a name="design-with-ui-templates"></a>UI テンプレートを使用した設計

UI テンプレートは、複雑で忠実度の高い設計で、一般的なTeamsワークフローに対応します。 基本的なコンポーネントから始める代わりに、これらのテンプレートを使用して設計プロセスを簡素化し、高速化することをお勧めします。

1. UI キットの左側のナビゲーションで **、[UI テンプレート] に移動します**。
1. アプリの設計に合ったテンプレートをコピーします。<br />
   たとえば、個人用アプリを設計する場合は、ダッシュボード テンプレートを使用できます。

### <a name="design-with-basic-ui-components"></a>基本的な UI コンポーネントを使用した設計

ユーザーインターフェイスFluent基づいて、使い慣れたインターフェイスを作成するためのTeams要素です。 UI テンプレートに必要なものが不足している場合や、アプリを最初から設計する場合は、これらのコンポーネントを使用します。

1. UI キットの左側のナビゲーションで、[基本 **UI コンポーネント] に移動します**。
1. アプリ設計に必要なコンポーネント (ボタンやトグルなど) をコピーします。

## <a name="implement-your-design"></a>デザインを実装する

デザインが完了し、構築を開始する準備が整いました。 次のツールは、アプリのフロントエンド開発を簡略化するのに役立ちます。

### <a name="build-with-ui-templates"></a>UI テンプレートを使用したビルド

デザインで UI テンプレートを使用した場合は、Microsoft Teams UI ライブラリ (React UI に基づく React コンポーネント ライブラリ) を使用してこれらのテンプレートをFluentできます。

現時点では、UI キットに一覧表示されているすべてのテンプレートがライブラリで使用できる場合ではありません。

> [!div class="nextstepaction"]
> [ライブラリを取得する (GitHub)](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="build-with-basic-ui-components"></a>基本的な UI コンポーネントを使用してビルドする

デザイン フェーズとは異なり、UI テンプレートに必要なものが不足している場合や、アプリを最初からビルドする場合は、アプリ プロジェクトでこれらの Fluent UI コンポーネントを使用できます。 

(注: 何かが見つからない場合や、テンプレートのアイデアがある場合は、UI ライブラリの repo にTeams検討してください)。

> [!div class="nextstepaction"]
> [ライブラリを取得する (Fluent UI)](https://fluentsite.z22.web.core.windows.net/)

## <a name="review-design-resources"></a>デザイン リソースを確認する

アプリを起動したばかりか、実稼働可能なアプリに近い場合でも、次のリソースを定期的に確認することをお勧めします。

* **Microsoft Teams検証** ガイドライン : ストアに表示されるアプリではなく、Teamsアプリが努力する必要がある標準を提供します。 詳細については、「ガイドライン」 [を参照してください](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)。
* **デザインのベスト プラクティス**: これらのドキュメントと UI キットは、高品質のアプリを設計するためのベスト プラクティスを提供します。 たとえば、ボットを設計 [するためのベスト プラクティスを参照してください](~/bots/design/bots.md#best-practices)。

