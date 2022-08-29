---
title: カスタム Azure Fluid Relay サービスを使用する方法
author: surbhigupta
description: このモジュールでは、Live Share でカスタム Azure Fluid Relay サービスを使用する方法について説明します。
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 07/21/2022
ms.openlocfilehash: baa192bf82e059b1cfe7a9fc8979874710f266b1
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425635"
---
---

# <a name="custom-azure-fluid-relay-service"></a>カスタム Azure Fluid Relay サービス

無料のホステッド サービスを使用することをお勧めしますが、Live Share アプリに独自の Azure Fluid Relay サービスを使用することが有益な状況があります。

## <a name="pre-requisites"></a>前提条件

1. [サイコロ ローラーのチュートリアル](../teams-live-share-tutorial.md)に示すように、会議サイド パネルとステージ アプリ会議拡張機能を構築します。
2. アプリ マニフェストを更新して [、必要なすべてのアクセス許可](../teams-live-share-capabilities.md#register-rsc-permissions)を含めます。
3. このチュートリアルで説明されているように、Azure Fluid Relay サービスをプロビジョニング [します](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal)。

## <a name="connect-to-azure-fluid-relay-service"></a>Azure Fluid Relay サービスに接続する

`TeamsFluidClient` クラスを作成するときに、独自の `AzureConnectionConfig` を定義できます。 Live Share では、作成したコンテナーが会議に関連付けられますが、コンテナーのトークンに署名するためのインターフェイスを実装 `ITokenProvider` する必要があります。 この例では、Azure `AzureFunctionTokenProvider`クラウド関数を使用してサーバーからアクセス トークンを要求する Azure について説明します。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralPresence } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";
import { AzureFunctionTokenProvider } from "@fluidframework/azure-client";

// Define a custom connection for your app
const clientProps = {
  connection: {
    tenantId: "MY_TENANT_ID",
    tokenProvider: new AzureFunctionTokenProvider(
      "MY_SERVICE_ENDPOINT_URL" + "/api/GetAzureToken",
      { userId: "userId", userName: "Test User" }
    ),
    endpoint: "MY_SERVICE_ENDPOINT_URL",
    type: "remote",
  },
};
// Join the Fluid container
const client = new TeamsFluidClient(clientProps);
const schema = {
  initialObjects: {
    presence: EphemeralPresence,
    ticTacToePositions: SharedMap,
  },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralPresence, ITeamsFluidClientOptions } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";
import { AzureFunctionTokenProvider } from "@fluidframework/azure-client";

// Define a custom connection for your app
const clientProps: ITeamsFluidClientOptions = {
  connection: {
    tenantId: "MY_TENANT_ID",
    tokenProvider: new AzureFunctionTokenProvider(
      "MY_FUNCTION_ENDPOINT_URL" + "/api/GetAzureToken",
      { userId: "userId", userName: "Test User" }
    ),
    endpoint: "MY_SERVICE_ENDPOINT_URL",
    type: "remote",
  },
};
// Join the Fluid container
const client = new TeamsFluidClient(clientProps);
const schema = {
  initialObjects: {
    presence: EphemeralPresence,
    ticTacToePositions: SharedMap,
  },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

---

## <a name="why-use-a-custom-azure-fluid-relay-service"></a>カスタム Azure Fluid Relay サービスを使用する理由

次の場合は、カスタム AFR サービス接続の使用を検討してください。

* 会議の有効期間を超えて、Fluid コンテナーにデータを格納する必要があります。
* カスタム セキュリティ ポリシーを必要とするサービスを介して機密データを送信します。
* Teams の外部でアプリケーション用の Fluid Framework を使用して機能を開発します。

## <a name="why-use-live-share-with-your-custom-service"></a>カスタム サービスで Live Share を使用する理由

Azure Fluid Relay は、任意の Web ベースのアプリケーションで動作するように設計されています。つまり、Microsoft Teams の有無にかかわらず動作します。 これは重要な問題です。自分で Azure Fluid Relay サービスを構築する場合、Live Share は引き続き必要ですか?

Live Share には、次のようなアプリ内の他の機能を強化する一般的な会議シナリオに役立つ機能があります。

* [コンテナーマッピング](#container-mapping)
* [エフェメラル オブジェクトとロール検証](#ephemeral-objects-and-role-verification)
* [メディア同期](#media-synchronization)

### <a name="container-mapping"></a>コンテナーマッピング

Live Share の `TeamsFluidClient` クラスは、一意の会議識別子を Fluid コンテナーにマッピングする役割を担います。これにより、すべての会議参加者が同じコンテナーに参加できるようになります。 このプロセスの一環として、クライアントは既に存在する `containerId` 会議にマップされた会議への接続を試みます。 存在しない場合は、コンテナーを`AzureClient`使用してコンテナーを作成し、それを他の`containerId`会議参加者に中継するために使用`AzureConnectionConfig`されます。

アプリに既に Fluid コンテナーを作成し、他のメンバーと共有するメカニズムがある場合 (会議ステージで共有されている URL に挿入 `containerId` するなど) は、アプリでは必要ない場合があります。

### <a name="ephemeral-objects-and-role-verification"></a>エフェメラル オブジェクトとロール検証

Live Share の一時的なデータ構造 (`EphemeralPresence`たとえば、`EphemeralState``EphemeralEvent`会議でのコラボレーションに合わせて調整されているため、Microsoft Teams の外部で使用される Fluid コンテナーではサポートされていません)。 ロール検証などの機能は、アプリがユーザーの期待に合わせて調整するのに役立ちます。

> [!NOTE]
> さらに利点として、一時的なオブジェクトは、従来の Fluid データ構造と比較して、メッセージの待機時間が速くなります。

詳細については、「 [コア機能](../teams-live-share-capabilities.md) 」ページを参照してください。

### <a name="media-synchronization"></a>メディア同期

パッケージは `@microsoft/live-share-media` 、Microsoft Teams の外部で使用される Fluid コンテナーではサポートされていません。

詳細については、「 [メディア機能](../teams-live-share-media-capabilities.md) 」ページを参照してください。

## <a name="see-also"></a>関連項目

* [GitHub リポジトリ](https://github.com/microsoft/live-share-sdk)
* [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
* [Live Share Media SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-media/)
* [Live Share 機能](../teams-live-share-capabilities.md)
* [Live Share 機能](../teams-live-share-media-capabilities.md)
* [Live Share FAQ](../teams-live-share-faq.md)
* [会議の Teams アプリ](../teams-apps-in-meetings.md)
