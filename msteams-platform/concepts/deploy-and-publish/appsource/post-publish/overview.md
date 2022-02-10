---
title: 公開したアプリの保守およびサポート
description: ストアがアプリ ストアと AppSource に一覧表示された後Teams考える必要があります。
ms.topic: conceptual
ms.localizationpriority: medium
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: cbb4eff47d21180bbdfe4aad49cb749a745386c2
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518563"
---
# <a name="maintain-your-published-microsoft-teams-app"></a>公開された Microsoft Teams アプリを管理する

アプリが Microsoft Teamsストアに表示された状態で、今後アプリを維持する方法について考え始め、ダウンロードと使用状況を増やします。

## <a name="publish-updates-to-your-app"></a>アプリに更新プログラムを発行する

> [!NOTE]
> Teamsが進化しました。
> 
> 以前は、アプリ タイルで省略記号を選択してリンクをコピーしました。 更新されたストア エクスペリエンスTeams、アプリの [詳細] タブから同じ情報にアクセスできます。 この更新プログラムは、2022 年 3 月 1 日までに一般提供 (GA) される予定です。

パートナー センターでは、アプリに変更 (新機能やメタデータなど) を送信できます。 これらの変更には、新しいレビュー プロセスが必要です。

更新プログラムを発行する場合は、次の情報を確認してください。

* アプリ ID を変更しない。
* アプリのバージョン番号を増やします。
* パートナー センターで、[新しいアプリの **追加] を選択して** 更新を行う必要があります。 代わりにアプリのページに移動します。

### <a name="app-updates-requiring-user-consent"></a>ユーザーの同意を必要とするアプリの更新

ユーザーがアプリをインストールする場合、アプリが機能するために必要なサービスと情報にアクセスするためのアクセス許可をアプリに付与する必要があります。 ほとんどの場合、ユーザーはこれを一度実行し、アプリの新しいバージョンが自動的にインストールされる必要があります。
ただし、アプリに次の変更を加えた場合、既存のユーザーは更新プログラムをインストールするための別のアクセス許可要求を受け入れる必要があります。

* ボットを追加または削除します。
* ボット ID を変更します。
* ボットの一方通行通知構成を変更します。
* ファイルのアップロードとダウンロードに関するボットのサポートを変更します。
* メッセージング拡張機能を追加または削除します。
* 個人用タブを追加します。
* [チャネルとグループ] タブを追加します。
* コネクタを追加します。
* アプリの登録に関連する構成Microsoft Azure Active Directory (Azure AD) を変更します。 詳細については、[`webApplicationInfo`](~/resources/schema/manifest-schema.md#webapplicationinfo) を参照してください。

## <a name="fix-issues-with-your-published-app"></a>発行済みアプリの問題を修正する

Microsoft は、アプリ ストアに一覧表示されているアプリで毎日自動化テストTeams実行します。 アプリに関する問題が特定された場合は、問題を再現する方法と問題を解決するための推奨事項に関する詳細なレポートをお客様に連絡します。 指定したタイムライン内で問題を解決できない場合は、アプリの登録情報がストアから削除される可能性があります。

## <a name="promote-your-app-on-another-site"></a>別のサイトでアプリを宣伝する

アプリが Teams ストアに表示されている場合は、Teamsを起動し、アプリをインストールするダイアログを表示するリンクを作成できます。 たとえば、製品のマーケティング ページにダウンロード ボタンを使用して、このリンクを含めできます。

アプリ ID に追加された次の URL を使用してリンクを作成します。 `https://teams.microsoft.com/l/app/<your-app-id>`

## <a name="complete-microsoft-365-certification"></a>完全なMicrosoft 365認定

[Microsoft 365認定は](/microsoft-365-app-certification/docs/certification)、サード パーティ製の Office アプリ またはアドインが Microsoft 365 エコシステムにインストールされている場合に、データとプライバシーが適切に保護され、保護されていることを保証します。 認定は、アプリが Microsoft テクノロジと互換性があり、クラウド アプリのセキュリティのベスト プラクティスに準拠しており、Microsoft によってサポートされていないことを確認します。

## <a name="see-also"></a>関連項目

[Microsoft Commercial Marketplace を通してアプリを収益化する](/office/dev/store/monetize-addins-through-microsoft-commercial-marketplace)
