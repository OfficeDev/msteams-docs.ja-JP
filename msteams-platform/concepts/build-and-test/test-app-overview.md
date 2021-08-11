---
title: アプリの概要をテストする
description: カスタム アプリをテストするプロセスTeams説明しますMicrosoft 365
ms.topic: how-to
localization_priority: Normal
keywords: テスト アプリMicrosoft 365アップロードTeamsテナントを構成する
ms.openlocfilehash: e33a1adb9ebc11f8bd1ece8f5fe43fc78e60b11883551fbd0ee3dfae237737cf
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57707690"
---
# <a name="test-your-app"></a>アプリのテスト

アプリとアプリを統合Microsoft Teams、アプリを発行する前にテストする必要があります。 最終的な目標は、アプリのユーザー数を多く取得し、ユーザーが使用できる複数のデバイスでアプリをテストする方法です。 アプリをテストする場合:

* テナントをMicrosoft 365します。
* アプリをテストおよびデバッグするワークスペースを選択します。
* テスト データをテナントにMicrosoft 365します。

## <a name="prepare-your-microsoft-365-tenant"></a>Microsoft 365 テナントを準備する

アプリのテストを開始する前に、テスト テナントMicrosoft 365準備し、アプリをアップロードできるカスタム Teamsを有効にします。 開発者プログラムにサインアップしMicrosoft 365組織のTeams管理する必要があります。 開発者サブスクリプションをセットアップし、テナントを準備[してMicrosoft 365します](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

## <a name="test-and-debug"></a>テストとデバッグ

アプリをテストおよびデバッグするには、少なくとも 1 つのワークスペースを作成する必要があります。 アプリをテストおよびデバッグするために、ローカル ホストやクラウドベースのホストなどのテストセットアップを選択できます。 アプリ エクスペリエンスを読みTeams実行するために、アプリをデバッグするガイダンスが提供されています。 詳細については、「セットアップを[選択してアプリを実行する」をMicrosoft Teamsしてください](~/concepts/build-and-test/debug.md)。

ボットをローカルでテストします。 詳細については [、「IDE を使用してボットをローカルでデバッグする」を参照してください](~/bots/how-to/debug/locally-with-an-ide.md)。 検査ミドルウェアとアダプティブ ツールを使用 [してボット](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) を [デバッグすることもできます](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)。 

コンソール ログを表示したり、実行時に html、css、およびネットワーク要求を表示または変更したりするには、JavaScript コードにブレークポイントを追加し、DevTools への対話的なデバッグ アクセスを実行します。 詳細については[、「Access the DevTools for the DevTools for the Teams」を参照してください](~/tabs/how-to/developer-tools.md)。 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>テスト データをテナントにMicrosoft 365する

テスト テナントにテスト データMicrosoft 365追加します。 詳細については、「テスト データをテスト テナントに追加する[Office 365、](~/concepts/build-and-test/test-data.md)テスト データのアップロードを開始する前に、すべての前提条件を完了する」を参照してください。

## <a name="see-also"></a>関連項目

* [タブをデバッグする](~/tabs/how-to/developer-tools.md)
* [ボットのデバッグ](~/bots/how-to/debug/locally-with-an-ide.md)
* [RSC のアクセス許可をテストする](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [Microsoft 365 テナントを準備する](~/concepts/build-and-test/prepare-your-o365-tenant.md)
