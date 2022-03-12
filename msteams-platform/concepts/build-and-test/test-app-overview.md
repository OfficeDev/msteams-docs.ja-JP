---
title: アプリの概要をテストする
description: カスタム アプリをテストおよびデバッグするプロセスTeams説明しますMicrosoft 365
ms.topic: how-to
ms.localizationpriority: medium
keywords: テスト アプリMicrosoft 365アップロードTeamsテナントを構成する
ms.openlocfilehash: 7831d245fd48b9eb5c6dd4761a84a1fee3d9cfef
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453881"
---
# <a name="test-your-app"></a>アプリのテスト

アプリを Microsoft Teams と統合した後、アプリを発行する前にテストする必要があります。 最終的な目標は、アプリのユーザー数を多く取得し、ユーザーが使用できる複数のデバイスでアプリをテストする方法です。 アプリをテストする場合:

* テナントを準備Microsoft 365します。
* アプリをテストおよびデバッグするワークスペースを選択します。
* テスト データをテナントにMicrosoft 365します。

## <a name="prepare-your-microsoft-365-tenant"></a>Microsoft 365 テナントを準備する

アプリのテストを開始する前に、テスト テナントMicrosoft 365準備し、アプリでアプリをアップロードTeamsカスタム テストを有効にします。 開発者プログラムにサインアップしMicrosoft 365組織のTeams管理する必要があります。 開発者サブスクリプションをセットアップし、テナントの準備[を通じてMicrosoft 365します](~/concepts/build-and-test/prepare-your-o365-tenant.md)。

## <a name="test-and-debug"></a>テストとデバッグ

アプリをテストおよびデバッグするには、少なくとも 1 つのワークスペースを作成する必要があります。 アプリをテストおよびデバッグするために、ローカル ホストやクラウドベースのホストなどのテストセットアップを選択できます。 アプリ エクスペリエンスを読みTeams実行するために、アプリをデバッグするガイダンスが提供されています。 詳細については、「セットアップを[選択してアプリを実行する」をMicrosoft Teamsしてください](~/concepts/build-and-test/debug.md)。

ボットをローカルでテストします。 詳細については、「IDE を [使用してボットをローカルでデバッグする」を参照してください](~/bots/how-to/debug/locally-with-an-ide.md)。 検査ミドルウェアとアダプティブ ツールを使用 [してボット](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) を [デバッグすることもできます](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)。

コンソール ログを表示したり、実行時に html、css、およびネットワーク要求を表示または変更したりするには、JavaScript コードにブレークポイントを追加し、DevTools への対話的なデバッグ アクセスを実行します。 詳細については、「[Access the DevTools for the DevTools for Teams参照してください](~/tabs/how-to/developer-tools.md)。

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>テスト データをテナントにMicrosoft 365する

テスト データをテスト テナントMicrosoft 365追加します。 詳細については、「テスト データを[テスト](~/concepts/build-and-test/test-data.md) テナントに追加Office 365テスト データのアップロードを開始する前に、すべての前提条件を完了する」を参照してください。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Microsoft 365 テナントを準備する](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="see-also"></a>関連項目

* [タブをデバッグする](~/tabs/how-to/developer-tools.md)
* [ボットのデバッグ](~/bots/how-to/debug/locally-with-an-ide.md)
* [RSC のアクセス許可をテストする](~/graph-api/rsc/test-resource-specific-consent.md)
