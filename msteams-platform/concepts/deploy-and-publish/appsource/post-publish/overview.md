---
title: 公開したアプリの保守およびサポート
description: 公開された Microsoft Teams アプリを管理します。 アプリの使用状況を分析し、更新プログラムを発行し、アプリを昇格し、Microsoft 365 認定を完了します。
ms.topic: conceptual
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: cbb97bd1fcd3422af968e7928436f4da1ae4038d
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615290"
---
# <a name="maintain-your-published-microsoft-teams-app"></a>公開された Microsoft Teams アプリを管理する

アプリが Microsoft Teams ストアにリストされたら、今後アプリを維持し、ダウンロードと使用量を増やす方法について考え始めます。

## <a name="analyze-app-usage"></a>アプリの使用状況を分析する

パートナー センターの [Teams アプリ使用状況レポート](/office/dev/store/teams-apps-usage)でアプリの使用状況を追跡できます。 メトリックには、月間、日単位、週単位のアクティブ ユーザー、リテンション期間と強度のグラフが含まれており、チャーンと使用量の頻度を追跡できます。

新しく公開されたアプリのデータがレポートに表示されるまでに約 1 週間かかります。

## <a name="publish-updates-to-your-app"></a>アプリに更新プログラムを発行する

パートナー センターでは、アプリに変更 (新機能やメタデータなど) を送信できます。 これらの変更には、新しいレビュー プロセスが必要です。

更新プログラムを発行する場合は、次の情報を確認してください。

* アプリ ID を変更しないでください。
* アプリのバージョン番号を増やします。
* In Partner Center, don't select **Add a new app** to do the update. Go to your app's page instead.

### <a name="app-updates-requiring-user-consent"></a>ユーザーの同意を必要とするアプリの更新

ユーザーがアプリをインストールする場合、アプリが機能するために必要なサービスと情報にアクセスするためのアクセス許可をアプリに付与する必要があります。 ほとんどの場合、ユーザーはこれを 1 回実行する必要があり、アプリの新しいバージョンが自動的にインストールされます。
ただし、アプリに次の変更を加えた場合、既存のユーザーは更新プログラムをインストールするための別のアクセス許可要求を受け入れる必要があります。

* ボットを追加または削除します。
* ボット ID を変更します。
* ボットの一方向の通知構成を変更します。
* ファイルのアップロードとダウンロードに対するボットのサポートを変更します。
* メッセージ拡張機能を追加または削除します。
* 個人用タブを追加します。
* チャネルとグループ タブを追加します。
* コネクタを追加します。
* Modify configurations related to your Microsoft Azure Active Directory (Azure AD) app registration. For more information, see [`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo).

## <a name="fix-issues-with-your-published-app"></a>公開したアプリの問題を修正する

Microsoft は、Teams ストアにリストされているアプリに対して毎日自動化テストを実行します。 アプリの問題が特定された場合は、問題を再現する方法に関する詳細なレポートと、問題を解決するための推奨事項についてご連絡します。 定められたタイムライン内に問題を修正できない場合、アプリのリストがストアから削除される可能性があります。

## <a name="promote-your-app-on-another-site"></a>別のサイトでアプリを宣伝する

アプリが Teams ストアに一覧表示されたら、Teams を起動し、アプリをインストールするためのダイアログを表示するリンクを作成できます。 たとえば、製品のマーケティング ページのダウンロード ボタンにこのリンクを含めることができます。

アプリ ID が付加された次の URL を使用してリンクを作成します: `https://teams.microsoft.com/l/app/<your-app-id>`。

## <a name="complete-microsoft-365-certification"></a>完全な Microsoft 365 認定

[Microsoft 365 認定](/microsoft-365-app-certification/docs/certification)は、サードパーティの Office アプリまたはアドインが Microsoft 365 エコシステムにインストールされている場合に、データとプライバシーが適切に保護されることを保証します。 認証により、アプリが Microsoft のテクノロジと互換性があり、クラウド アプリのセキュリティのベスト プラクティスに準拠し、Microsoft によってサポートされていることが確認されます。

## <a name="stop-app-distribution"></a>アプリの配布を停止する

[Microsoft コマーシャル マーケットプレース](/azure/marketplace/overview)からアプリを削除して、その検出と使用を防ぐことができます。

発行後にアプリの配布を停止するには、次の手順に従います:

1. [**製品の概要**] ページで、[**販売の停止**] を選択します。 Microsoft AppSource からアプリを削除します。
1. アプリの登録解除を開始するには、 **パートナー センター** で [**概要**] ページを選択し、[**販売の停止**] を選択します。

アプリの配布を停止した後も、パートナー センターで [**使用不可]** 状態で表示されます。 アプリをもう一度一覧表示する場合は、指示に従って[アプリをMicrosoft Teams ストアに発行します](../publish.md)。

## <a name="see-also"></a>関連項目

[Microsoft Commercial Marketplace を通してアプリを収益化する](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
