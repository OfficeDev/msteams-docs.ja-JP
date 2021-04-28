---
title: アプリの概要をテストする
description: Microsoft 365 で Teams カスタム アプリをテストするプロセスについて説明します。
ms.topic: how-to
localization_priority: Normal
keywords: テスト アプリをアップロードする Microsoft 365 テナント Teams を構成する
ms.openlocfilehash: d95d65961b060ff1938d51c0f3fafc2b1e56fa7e
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058608"
---
# <a name="test-your-app"></a>アプリのテスト

アプリを Microsoft Teams と統合した後、アプリを発行する前にテストする必要があります。 最終的な目標は、アプリのユーザー数を多く取得し、ユーザーが使用できる複数のデバイスでアプリをテストする方法です。 アプリをテストする場合:

* Microsoft 365 テナントを準備する
* アプリをテストおよびデバッグするワークスペースを選択する
* テスト データを Microsoft 365 テナントに追加する

## <a name="prepare-your-microsoft-365-tenant"></a>Microsoft 365 テナントを準備する

アプリのテストを開始する前に、Microsoft 365 テスト テナントを準備し、カスタム Teams アプリを有効にしてアプリをアップロードできます。 Microsoft 365 開発者プログラムにサインアップし、組織の Teams 設定を管理する必要があります。 開発者サブスクリプションをセットアップし [、Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)テナントを準備して構成します。

## <a name="test-and-debug"></a>テストとデバッグ

アプリをテストおよびデバッグするには、少なくとも 1 つのワークスペースを作成する必要があります。 アプリをテストおよびデバッグするために、ローカル ホストやクラウドベースのホストなどのテストセットアップを選択できます。 Teams アプリをデバッグするガイダンスは、アプリ エクスペリエンスを読み込み、実行するために提供されます。 詳細については、「セットアップを [選択して Microsoft Teams アプリを実行する」を参照してください](~/concepts/build-and-test/debug.md)。

ボットをローカルでテストします。 詳細については [、「IDE を使用してボットをローカルでデバッグする」を参照してください](~/bots/how-to/debug/locally-with-an-ide.md)。 検査ミドルウェアとアダプティブ ツールを使用 [してボット](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) を [デバッグすることもできます](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)。 

コンソール ログを表示したり、実行時に html、css、およびネットワーク要求を表示または変更したりするには、JavaScript コードにブレークポイントを追加し、DevTools への対話的なデバッグ アクセスを実行します。 詳細については [、「Access the DevTools for Teams」タブを参照してください](~/tabs/how-to/developer-tools.md)。 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>テスト データを Microsoft 365 テナントに追加する

テスト データを Microsoft 365 テスト テナントに追加します。 詳細については、「テスト データを Office [365](~/concepts/build-and-test/test-data.md)テスト テナントに追加し、テスト データのアップロードを開始する前に、すべての前提条件を完了する」を参照してください。

## <a name="see-also"></a>関連項目

- [タブをデバッグする](~/tabs/how-to/developer-tools.md)
 
- [ボットのデバッグ](~/bots/how-to/debug/locally-with-an-ide.md)

- [RSC のアクセス許可をテストする](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Microsoft 365 テナントを準備する](~/concepts/build-and-test/prepare-your-o365-tenant.md)
