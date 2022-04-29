---
title: 公開したアプリの保守およびサポート
description: あなたの店が Teams ストアと AppSource にリストされたら考えること。
ms.topic: conceptual
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 2a85739a5a94109aae87de4579f17fe99df8d28b
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104533"
---
# <a name="maintain-your-published-microsoft-teams-app"></a>公開された Microsoft Teams アプリを管理する

アプリが Microsoft Teams ストアにリストされたら、今後アプリを維持し、ダウンロードと使用量を増やす方法について考え始めます。

## <a name="analyze-app-usage"></a>アプリの使用状況を分析する

パートナー センターの [Teams アプリ使用状況レポート](/office/dev/store/teams-apps-usage)でアプリの使用状況を追跡できます。 メトリックには、月間、日単位、週単位のアクティブ ユーザー、リテンション期間と強度のグラフが含まれており、チャーンと使用量の頻度を追跡できます。

新しく公開されたアプリのデータがレポートに表示されるまでに約 1 週間かかります。

## <a name="publish-updates-to-your-app"></a>アプリに更新プログラムを発行する

> [!NOTE]
> Teams ストアが進化しました。
>
> 以前は、アプリ タイルで省略記号を選択してリンクをコピーしました。 更新された Teams ストア エクスペリエンスを使用すると、アプリの [詳細] タブから同じものにアクセスできます。 この更新プログラムは、2022 年 3 月 1 日までに一般提供 (GA) される予定です。

パートナー センターでは、アプリに変更 (新機能やメタデータなど) を送信できます。これらの変更には、新しいレビュー プロセスが必要です。

更新プログラムを発行する場合は、次の情報を確認してください。

* アプリ ID を変更しないでください。
* アプリのバージョン番号を増やします。
* パートナー センターで、更新を行うために **[新しいアプリの追加]** を選択しないでください。代わりにアプリのページに移動します。

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
* Microsoft Azure Active Directory (Azure AD) アプリの登録に関連する構成を変更します。詳細については、「[`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo)」を参照してください。

## <a name="fix-issues-with-your-published-app"></a>公開したアプリの問題を修正する

Microsoft は、Teams ストアにリストされているアプリに対して毎日自動化テストを実行します。 アプリの問題が特定された場合は、問題を再現する方法に関する詳細なレポートと、問題を解決するための推奨事項についてご連絡します。 定められたタイムライン内に問題を修正できない場合、アプリのリストがストアから削除される可能性があります。

## <a name="promote-your-app-on-another-site"></a>別のサイトでアプリを宣伝する

アプリが Teams ストアに一覧表示されたら、Teams を起動し、アプリをインストールするためのダイアログを表示するリンクを作成できます。 たとえば、製品のマーケティング ページのダウンロード ボタンにこのリンクを含めることができます。

アプリ ID が付加された次の URL を使用してリンクを作成します: `https://teams.microsoft.com/l/app/<your-app-id>`。

## <a name="complete-microsoft-365-certification"></a>完全な Microsoft 365 認定

[Microsoft 365 認定](/microsoft-365-app-certification/docs/certification)は、サードパーティの Office アプリまたはアドインが Microsoft 365 エコシステムにインストールされている場合に、データとプライバシーが適切に保護されることを保証します。 認証により、アプリが Microsoft のテクノロジと互換性があり、クラウド アプリのセキュリティのベスト プラクティスに準拠し、Microsoft によってサポートされていることが確認されます。

## <a name="see-also"></a>関連項目

[Microsoft Commercial Marketplace を通してアプリを収益化する](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
