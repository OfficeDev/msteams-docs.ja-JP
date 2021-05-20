---
title: アプリの概要をテストする
description: Teamsカスタム アプリをテストするプロセスMicrosoft 365
ms.topic: how-to
localization_priority: Normal
keywords: テスト アプリMicrosoft 365アップロードTeamsテナントを構成する
ms.openlocfilehash: 2c9f23a5c6ae286ff4b7d911f370bd45b854a647
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565187"
---
# <a name="test-your-app"></a>アプリのテスト

アプリをMicrosoft Teamsに統合したら、アプリを公開する前にテストする必要があります。 最終的な目標は、アプリのユーザー数をできるだけ多く取得し、ユーザーが使用できる複数のデバイスでアプリをテストすることです。 アプリのテスト:

* Microsoft 365テナントを準備します。
* アプリをテストおよびデバッグするワークスペースを選択します。
* Microsoft 365テナントにテスト データを追加します。

## <a name="prepare-your-microsoft-365-tenant"></a>Microsoft 365 テナントを準備する

アプリのテストを開始する前に、Microsoft 365テスト テナントを準備し、カスタム Teams アプリを有効にすると、アプリをアップロードできます。 開発者プログラムMicrosoft 365サインアップし、組織のTeams設定を管理する必要があります。 開発者サブスクリプションを設定し[、Microsoft 365テナントを準備して構成します](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

## <a name="test-and-debug"></a>テストとデバッグ

アプリをテストおよびデバッグするには、少なくとも 1 つのワークスペースを作成する必要があります。 ローカル ホストやクラウドベースのホストなど、テストのセットアップを選択して、アプリをテストおよびデバッグできます。 アプリの読み込みと実行にTeamsアプリをデバッグするためのガイダンスが提供されます。 詳細については、「[設定を選択して、Microsoft Teams アプリを実行する」を](~/concepts/build-and-test/debug.md)参照してください。

ボットをローカルでテストします。 詳細については、「 IDE を [使用してボットをローカルでデバッグする](~/bots/how-to/debug/locally-with-an-ide.md)」を参照してください。 検査 [ミドルウェア](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) や [適応ツール](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)を使用してボットをデバッグすることもできます。 

コンソール ログを表示したり、実行時に html、css、およびネットワーク要求を表示または変更したりするには、JavaScript コードにブレークポイントを追加し、デバッグに関する対話的なアクセスを実行します。 詳細については、「 [Teamsの DevTools タブにアクセスする](~/tabs/how-to/developer-tools.md)」を参照してください。 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Microsoft 365テナントにテスト データを追加する

テスト データをテスト テナントに追加Microsoft 365。 詳細については、「テスト[データを Office 365テスト テナントに追加する」](~/concepts/build-and-test/test-data.md)を参照し、テスト データのアップロードを開始する前にすべての前提条件を完了します。

## <a name="see-also"></a>関連項目

- [タブをデバッグする](~/tabs/how-to/developer-tools.md)
 
- [ボットをデバッグする](~/bots/how-to/debug/locally-with-an-ide.md)

- [RSC 権限のテスト](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Microsoft 365 テナントを準備する](~/concepts/build-and-test/prepare-your-o365-tenant.md)
