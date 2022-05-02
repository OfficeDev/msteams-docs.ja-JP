---
title: アプリの概要をテストする
description: Microsoft 365 で Teams カスタム アプリをテストしてデバッグするプロセスについて説明します。
ms.topic: how-to
ms.localizationpriority: high
keywords: テスト アプリをアップロードする Microsoft 365 テナント チームを構成する
ms.openlocfilehash: 98c00ece54e1654570556bac122e6760b283b73f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111529"
---
# <a name="test-your-app"></a>アプリのテスト

アプリを Microsoft Teams と統合した後、アプリを発行する前にテストする必要があります。 最終的な目標は、アプリのユーザーをできるだけ多く獲得することです。したがって、ユーザーが使用できる複数のデバイスでアプリをテストするようにしてください。 アプリをテストする場合:

* Microsoft 365 テナントを準備する
* アプリをテストしてデバッグするワークスペースを選択します。
* Microsoft 365 テナントにテスト データを追加する

## <a name="prepare-your-microsoft-365-tenant"></a>Microsoft 365 テナントを準備する

アプリのテストを開始する前に、Microsoft 365 テスト テナントを準備し、カスタム Teams アプリを有効にすると、アプリをアップロードできます。 Microsoft 365 開発者プログラムにサインアップし、組織の Teams 設定を管理する必要があります。 開発者サブスクリプションを設定し、[Microsoft 365 テナントを準備](~/concepts/build-and-test/prepare-your-o365-tenant.md)して構成します。

## <a name="test-and-debug"></a>テストとデバッグ

アプリをテストしてデバッグするには、少なくとも 1 つのワークスペースを作成する必要があります。 テストセットアップ (ローカル ホストやクラウドベースのホストなど) を選択して、アプリをテストおよびデバッグできます。 アプリ エクスペリエンスを読み込んで実行するために、Teams アプリをデバッグするためのガイダンスが提供されています。 詳細については、「[セットアップを選択して、Microsoft Teams アプリを実行する](~/concepts/build-and-test/debug.md)」を参照してください。

ボットをローカルでテストします。 詳細については、「[IDE を使用してボットをローカルでデバッグする](~/bots/how-to/debug/locally-with-an-ide.md)」を参照してください。 また、[検査ミドルウェア](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)と[アダプティブ ツール](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true)を使用してボットをデバッグすることもできます。

コンソール ログを表示するには、実行時に html、css、およびネットワーク リクエストを表示または変更し、JavaScript コードにブレーク ポイントを追加し、DevTools にインタラクティブなデバッグ アクセスを実行します。 詳細については、「[Teams タブの DevTools へのアクセス](~/tabs/how-to/developer-tools.md)」を参照してください。

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Microsoft 365 テスト テナントにテスト データを追加する

Microsoft 365 テスト テナントにテスト データを追加します。 詳細については、「[テスト データをOffice 365テスト テナントに追加する](~/concepts/build-and-test/test-data.md)」を参照し、テスト データのアップロードを開始する前にすべての前提条件を満たしてください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [Microsoft 365 テナントを準備する](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="see-also"></a>関連項目

* [DevTools でタブのデバッグを行う](~/tabs/how-to/developer-tools.md)
* [ボットをデバッグする](~/bots/how-to/debug/locally-with-an-ide.md)
* [RSC のアクセス許可をテストする](~/graph-api/rsc/test-resource-specific-consent.md)
