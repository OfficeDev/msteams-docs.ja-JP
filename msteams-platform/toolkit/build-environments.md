---
title: Teams Toolkit を使用してアプリをビルドする準備をする
author: surbhigupta
description: この記事では、Teams Toolkit の環境を構築し、開発者ポータルでアプリを管理する方法について説明します。
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: dc3a51d393a6445c26dddd54c471ecb630580b94
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806909"
---
# <a name="prepare-to-build-apps-using-teams-toolkit"></a>Teams Toolkit を使用してアプリをビルドする準備をする

Teams Toolkit では、アプリを作成するための環境がサポートされています。 Teams Toolkit は、Azure Functions機能とクラウド サービスを構築した Teams アプリに統合するのにも役立ちます。

:::image type="content" source="../assets/images/buildapps-TTK.png" alt-text="Teams Toolkit を使用してアプリをビルドする準備をする":::

## <a name="build-environments"></a>ビルド環境

Microsoft Visual Studio Code の Teams Toolkit には、Teams アプリを構築するための一連の環境が用意されています。 アプリに最適な次の環境の任意のユーザーを選択できます。

* JavaScript または TypeScript
* SharePoint Framework (SPFx)

### <a name="create-your-teams-app-using-javascript-or-typescript"></a>JavaScript または TypeScript を使用して Teams アプリを作成する

JavaScript でビルドされたアプリには、次の利点があります。

* アプリには、豊富でユーザー フレンドリな独自の UI および UX 機能が付属しています。
* 既存のアプリへの迅速なアップグレードを提供します。
* Android や iOS などの複数のプラットフォームにアプリを配布します。
* 既存の API を使用してアプリを作成する場合に互換性があります。

Visual Studio Code の Teams Toolkit では、JavaScript または TypeScript を使用して次のアプリをビルドできます。

* タブ アプリ: タブ アプリには Web ベースのコンテンツを含めることができます。Teams で Web コンテンツのカスタム タブを作成したり、Teams 固有の機能を Web コンテンツに追加したりできます。
* ボット アプリ: ボットは、顧客サービスやサポート スタッフなどの簡単で反復的なタスクを実行できるチャット ボットまたは会話型ボットにすることができます。
* 通知ボット: Http 要求を使用して、通知ボットによって Teams チャネルまたはグループまたは個人用チャットでメッセージを送信できます。
* コマンド ボット: コマンド ボットを使用して、繰り返しタスクを自動化できます。 コマンド ボットは、チャットで送信された簡単なクエリやコマンドに回答するのに役立ちます。
* メッセージ拡張機能: ボタンとフォームを使用して Web サービスを操作できます。 メッセージ拡張機能によって提供される機能。

### <a name="create-your-teams-app-using-spfx"></a>SPFx を使用して Teams アプリを作成する

Visual Studio Code の Teams Toolkit では、SPFx を使用してタブ アプリを作成できます。 これらのアプリには、次の利点があります。

* SharePoint に存在するデータを Teams に簡単に統合できます。
* SPFx ソリューションを、Microsoft Azure Active Directory (Azure AD) でセキュリティで保護されたビジネス API と統合できます。
* さまざまなオープン ソース ツールにアクセスできます。
* 優れた UX を提供できる強力なアプリケーションを作成します。
* 他の Microsoft (Office) 365 ワークロードと簡単に統合できます。
* 必要に応じて、アプリケーションをホストする柔軟性を提供します。

## <a name="support-for-azure-functions"></a>Azure Functionsのサポート

Teams Toolkit を使用して[、Azure Functions](/azure/azure-functions/functions-overview)機能をアプリの構築に統合できます。 最も重要なコードの部分に焦点を当て、残りの部分Azure Functions行うことができます。
Azure Functions実装できます。

1. すぐに使用できるコード ブロックにシステム ロジックを組み込みます。 これらのブロックは関数と呼ばれます。
1. 要求が増えるにつれて、Azure Functionsは必要な数の要求で要件を満たします。

Azure Function は、さまざまな [クラウド サービス](add-resource.md#types-of-cloud-resources) と統合され、機能豊富な実装を提供します。 Azure Functionsの一般的なシナリオを次に示します。

* Web API を構築する場合
* データベース変更への処理
* Iot データ ストリームの処理
* メッセージ キューの管理

## <a name="see-also"></a>関連項目

* [Visual Studio 用 Teams ツールキット](visual-studio-overview.md)
* [開発者ポータルを使用して Teams アプリを管理する](../concepts/build-and-test/teams-developer-portal.md)
* [Teams Toolkit を使用して新しい Teams アプリを作成する](create-new-project.md)
