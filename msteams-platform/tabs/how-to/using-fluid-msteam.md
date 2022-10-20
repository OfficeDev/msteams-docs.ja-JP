---
title: Teams で Fluid を使用する
author: timtwang
ms.author: mobajemu
description: Fluid を使用したリアルタイム コラボレーション機能を Microsoft Teams タブ アプリケーションに統合するためのチュートリアル
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 620e2150ca6300fb8d37bc7c68b965aacb19700b
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615441"
---
# <a name="use-fluid-with-teams"></a>Teams で Fluid を使用する

このチュートリアルの終わりまでに、Fluid を使用するアプリケーションを Teams に統合し、他のユーザーとリアルタイムで共同作業することができます。

このセクションでは、次の概念について説明します。

1. Fluid クライアントを Teams タブ アプリケーションに統合します。
1. Teams アプリケーションを実行し、Fluid サービス (Azure Fluid Relay) に接続します。
1. Fluid Containers を作成して取得し、React コンポーネントに渡します。

複雑なアプリケーションを構築する方法の詳細については、FluidExamples リポジトリの [Teams Fluid Hello World](https://github.com/microsoft/FluidExamples/tree/main/teams-fluid-hello-world)例を参照してください。

## <a name="prerequisites"></a>前提条件

このチュートリアルでは、次の概念とリソースに精通している必要があります。

- [Fluid Framework の概要](https://fluidframework.com/docs/)
- [Fluid Framework QuickStart](https://fluidframework.com/docs/start/quick-start/)
- [React](https://reactjs.org/)フックと[React フックの](https://reactjs.org/docs/hooks-intro.html)基本
- [Microsoft Teams タブ](/microsoftteams/platform/tabs/what-are-tabs)を作成する方法

> [!div class="nextstepaction"]
> [前提条件のインストール](tab-requirements.md)

## <a name="create-the-project"></a>プロジェクトを作成する

1. コマンド プロンプトを開き、プロジェクトを作成する親フォルダーに移動します 。たとえば、 `/My Microsoft Teams Projects`
1. 次のコマンドを実行し、 [チャネル タブを作成して Teams タブ アプリケーションを作成します](create-channel-group-tab.md#create-a-custom-channel-or-group-tab-with-nodejs)。

    ```cmd
    yo teams
    ```

1. 作成後、次のコマンドを使用してプロジェクトに移動します `cd <your project name>`。
1. プロジェクトでは、次のライブラリが使用されます。

    |ライブラリ |説明 |
    |---|---|
    | `fluid-framework`    |IFluidContainer と、クライアント間でデータを同期するその他 [の分散データ構造](https://fluidframework.com/docs/build/dds/) を格納します。|
    | `@fluidframework/azure-client`   |[Fluid コンテナー](https://fluidframework.com/docs/build/containers/)の開始スキーマを定義します。|
    | `@fluidframework/test-client-utils` |`InsecureTokenProvider` Fluid サービスへの接続を作成するために必要な値を定義します。|

    次のコマンドを実行してライブラリをインストールします。

    ```cmd
    npm install @fluidframework/azure-client fluid-framework @fluidframework/test-client-utils
    ```

## <a name="code-the-project"></a>プロジェクトをコーディングする

1. コード エディターでファイル `/src/client/<your tab name>` を開きます。
1. 新しいファイル `Util.ts` を作成し、次の import ステートメントを追加します。

    ```ts
    //`Util.ts

    import { IFluidContainer } from "fluid-framework";
    import { AzureClient, AzureClientProps } from "@fluidframework/azure-client";
    import { InsecureTokenProvider } from "@fluidframework/test-client-utils";
    ```

### <a name="defining-fluid-functions-and-parameters"></a>Fluid 関数とパラメーターの定義

このアプリは、すべての Fluid 関連のインポート、初期化、および関数を組み合わせて、Microsoft Teams のコンテキストで使用することを目的としています。 これにより、エクスペリエンスが強化され、将来の使用が容易になります。 import ステートメントに次のコードを追加できます。

```ts
// TODO 1: Define the parameter key(s).
// TODO 2: Define container schema.
// TODO 3: Define connectionConfig (AzureClientProps).
// TODO 4: Create Azure client.
// TODO 5: Define create container function.
// TODO 6: Define get container function.
```

> [!NOTE]
> コメントでは、Fluid サービスとコンテナーとの対話に必要なすべての関数と定数を定義します。

1. `TODO 1:` を次のコードに置き換えます。

    ```ts
    export const containerIdQueryParamKey = "containerId";
    ```

    定数は、Microsoft Teams の設定に `contentUrl` 追加され、後でコンテンツ ページのコンテナー ID を解析するためにエクスポートされます。 重要なクエリ パラメーター キーは、毎回生の文字列を入力するのではなく、定数として格納するのが一般的なパターンです。

    クライアントがコンテナーを作成するには、このアプリケーションで使用される共有オブジェクトを定義するコンテナーが必要 `containerSchema` です。 この例では SharedMap を使用しますが、任意の `initialObjects`共有オブジェクトを使用できます。

    > [!NOTE]
    > オブジェクト `map` の `SharedMap` ID であり、コンテナー内で他の DDS として一意である必要があります。

1. `TODO: 2` を次のコードに置き換えます。

    ```ts
    const containerSchema = {
        initialObjects: { map: SharedMap }
    };
    ```

1. `TODO: 3` を次のコードに置き換えます。

    ```ts
    const connectionConfig : AzureClientProps =
    {
        connection: {
            type: "local",
            tokenProvider: new InsecureTokenProvider("foobar", { id: "user" }),
            endpoint: "http://localhost:7070"
        }
    };
    ```

    クライアントを使用するには、クライアントが使用する `AzureClientProps` 接続の種類を定義する必要があります。 このプロパティは `connectionConfig` 、サービスに接続するために必要です。 Azure クライアントのローカル モードが使用されます。 すべてのクライアント間でコラボレーションを有効にするには、それを Fluid Relay Service 資格情報に置き換えます。 詳細については、 [Azure Fluid Relay サービスを設定する](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal)方法について説明します。

1. `TODO: 4` を次のコードに置き換えます。

    ```ts
    const client = new AzureClient(connectionConfig);
    ```

1. `TODO: 5` を次のコードに置き換えます。

    ```ts
    export async function createContainer() : Promise<string> {
        const { container } = await client.createContainer(containerSchema);
        const containerId = await container.attach();
        return containerId;
    };
    ```

    構成ページでコンテナーを作成し、それを Teams の設定に `contentUrl` 追加するときに、コンテナーをアタッチした後にコンテナー ID を返す必要があります。

1. `TODO: 6` を次のコードに置き換えます。

    ```ts
    export async function getContainer(id : string) : Promise<IFluidContainer> {
        const { container } = await client.getContainer(id, containerSchema);
        return container;
    };
    ```

    Fluid コンテナーをフェッチするときは、アプリケーションがコンテナーとコンテナー内の DDS をコンテンツ ページで操作する必要があるため、コンテナーを返す必要があります。

### <a name="create-fluid-container-in-the-configuration-page"></a>構成ページで Fluid コンテナーを作成する

1. コード エディターでファイル `src/client/<your tab name>/<your tab name>Config.tsx` を開きます。

    標準の Teams タブ アプリケーション フローは、構成からコンテンツ ページに移動します。 コラボレーションを有効にするには、コンテンツ ページへの読み込み中にコンテナーを保持することが重要です。 コンテナーを保持する最適な解決策は、コンテナー ID をクエリ パラメーターとしてコンテンツ ページの URL と URL に`contentUrl``websiteUrl`追加することです。 Teams 構成ページの [保存] ボタンは、構成ページとコンテンツ ページの間のゲートウェイです。 コンテナーを作成し、設定にコンテナー ID を追加する場所です。

1. 次の import ステートメントを追加します:

    ```ts
    import { createContainer, containerIdQueryParamKey } from "./Util";
    ```

1. `onSaveHandler` メソッドを次のコードに置き換えます。 ここで追加する行は、前 `Utils.ts` に定義したコンテナーの作成メソッドを呼び出し、返されたコンテナー ID を `contentUrl` クエリ パラメーターとして `websiteUrl` 追加することです。

    ```ts {linenos=inline,hl_lines=[134,136,137]}
    const onSaveHandler = async (saveEvent: microsoftTeams.settings.SaveEvent) => {
        const host = "https://" + window.location.host;
        const containerId = await createContainer();
        microsoftTeams.settings.setSettings({
            contentUrl: host + "/<your tab name>/?" + containerIdQueryParamKey + "=" + containerId + "&name={loginHint}&tenant={tid}&group={groupId}&theme={theme}",
            websiteUrl: host + "/<your tab name>/?" + containerIdQueryParamKey + "=" + containerId + "&name={loginHint}&tenant={tid}&group={groupId}&theme={theme}",
            suggestedDisplayName: "<your tab name>",
            removeUrl: host + "/<your tab name>/remove.html?theme={theme}",
            entityId: entityId.current
        });
        saveEvent.notifySuccess();
    };
    ```

    プロジェクトのタブ名に必ず置き換えてください `<your tab name>` 。

    > [!WARNING]
    > コンテンツ ページ URL を使用してコンテナー ID を格納すると、Teams タブが削除されると、このレコードが削除されます。
    > さらに、すべてのコンテンツ ページでサポートできるコンテナー ID は 1 つだけです。

### <a name="refactor-content-page-to-reflect-fluid-application"></a>Fluid アプリケーションを反映するようにコンテンツ ページをリファクタリングする

1. コード エディターでファイル `src/client/<your tab name>/<your tab name>.tsx` を開きます。 一般的な Fluid を使用するアプリケーションは、ビューと Fluid データ構造で構成されます。 Fluid コンテナーの取得と読み込みに重点を置き、React コンポーネント内のすべての Fluid 関連の相互作用を残します。

1. コンテンツ ページに次の import ステートメントを追加します。

    ```ts
    import { IFluidContainer } from "fluid-framework";
    import { getContainer, containerIdQueryParamKey } from "./Util";
    ```

1. コンテンツ ページの import ステートメントの下にあるすべてのコードを削除し、次のコードに置き換えます。

    ```ts
    export const <your tab name> = () => {
      // TODO 1: Initialize Microsoft Teams.
      // TODO 2: Initialize inTeams boolean.
      // TODO 3: Define container as a React state.
      // TODO 4: Define a method that gets the Fluid container
      // TODO 5: Get Fluid container on content page startup.
      // TODO 6: Pass the container to the React component as argument.
    }
    ```

    プロジェクトに対して定義したタブ名に必ず置き換えてください `<your tab name>` 。

1. `TODO 1` を次のコードに置き換えます。

    ```ts
    microsoftTeams.initialize();
    ```

    Teams でコンテンツ ページを表示するには、 [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client) を含め、ページの読み込み後に初期化する呼び出しを含める必要があります。

1. `TODO 2` を次のコードに置き換えます。

    ```ts
    const [{ inTeams }] = useTeams();
    ```

    Teams アプリケーションは単なる Web ページの IFrame インジェクションであるため、アプリケーションが Teams 内にあるかどうか、および Teams リソース (例: Teams リソース) が使用可能かどうかを確認するために、ブール定数を初期化 `inTeams` する `contentUrl`必要があります。

1. `TODO 3` を次のコードに置き換えます。

    ```ts
    const [fluidContainer, setFluidContainer] = useState<IFluidContainer | undefined>(undefined);
    ```

    コンテナーとそのコンテナー内のデータ オブジェクトを動的に更新する機能を提供するため、コンテナーのReact状態を使用します。

1. `TODO 4` を次のコードに置き換えます。

    ```ts
    const getFluidContainer = async (url : URLSearchParams) => {
        const containerId = url.get(containerIdQueryParamKey);
        if (!containerId) {
            throw Error("containerId not found in the URL");
        }
        const container = await getContainer(containerId);
        setFluidContainer(container);
    };
    ```

    URL を分析してクエリ パラメーター文字列を取得し、コンテナー ID を `containerIdQueryParamKey`取得します。 コンテナー ID を使用して、コンテナーを読み込むことができます。 コンテナーを作成したら、React状態を`fluidContainer`設定します。前の手順を参照してください。

1. `TODO 5` を次のコードに置き換えます。

    ```ts
    useEffect(() => {
        if (inTeams === true) {
            microsoftTeams.settings.getSettings(async (instanceSettings) => {
                const url = new URL(instanceSettings.contentUrl);
                getFluidContainer(url.searchParams);
            });
            microsoftTeams.appInitialization.notifySuccess();
        }
    }, [inTeams]);
    ```

    Fluid コンテナーを取得する方法を定義したら、読み込み時に呼び出`getFluidContainer`すようにReactに指示し、アプリケーションが Teams 内にあるかどうかに基づいて結果を状態で格納する必要があります。
    Reactの [useState フック](https://reactjs.org/docs/hooks-state.html)は必要なストレージを提供し、[useEffect](https://reactjs.org/docs/hooks-effect.html) を使用すると、返された値`setFluidContainer`を `getFluidContainer` .

    アプリの末尾に依存関係配列を追加 `inTeams` することで、この関数がコンテンツ ページの `useEffect`読み込みでのみ呼び出されるようにします。

1. `TODO 6` を次のコードに置き換えます。

    ```ts
    if (inTeams === false) {
      return (
          <div>This application only works in the context of Microsoft Teams</div>
      );
    }

    if (fluidContainer !== undefined) {
      return (
          <FluidComponent fluidContainer={fluidContainer} />
      );
    }

    return (
      <div>Loading FluidComponent...</div>
    );
    ```

    > [!NOTE]
    > コンテンツ ページが Teams 内に読み込まれ、Fluid コンテナーが定義されていることを確認してから、React コンポーネントに渡すことが重要です (`FluidComponent`以下を参照)。

### <a name="create-react-component-for-fluid-view-and-data"></a>Fluid ビューとデータのReact コンポーネントを作成する

Teams と Fluid の基本的な作成フローを統合しました。 これで、アプリケーション ビューと Fluid データの間の相互作用を処理する独自のReact コンポーネントを作成できるようになりました。 現時点では、ロジックとフローは、他の Fluid を使用するアプリケーションと同様に動作します。 基本構造を設定すると、コンテンツ ページの DDSes/データ オブジェクトとアプリケーション ビューの相互作用を変更`ContainerSchema`することで、Teams アプリケーションとして[任意の Fluid の例](https://github.com/microsoft/FluidExamples)を作成できます。

## <a name="start-the-fluid-server-and-run-the-application"></a>Fluid サーバーを起動し、アプリケーションを実行する

Azure クライアント ローカル モードで Teams アプリケーションをローカルで実行している場合は、コマンド プロンプトで次のコマンドを実行して、Fluid サービスを開始してください。

```cmd
npx @fluidframework/azure-local-service@latest
```

Teams アプリケーションを実行して起動するには、別のターミナルを開き、 [指示に従ってアプリケーション サーバーを実行します](create-channel-group-tab.md#upload-your-application-to-teams)。

> [!WARNING]
> 's free tunnels を持つ `ngrok`HostNames は保持されません。 実行ごとに異なる URL が生成されます。 新しい `ngrok` トンネルが作成されると、古いコンテナーにアクセスできなくなります。 運用シナリオについては、「 [Azure Fluid Relay で AzureClient を使用](#use-azureclient-with-azure-fluid-relay)する」を参照してください。

> [!NOTE]
> このデモを Webpack 5 と互換性のあるものにするために、追加の依存関係をインストールします。 "buffer" パッケージに関連するコンパイル エラーが発生した場合は、実行 `npm install -D buffer` して再試行してください。 これは、今後のリリースの Fluid Framework で解決される予定です。

## <a name="next-steps"></a>次の手順

### <a name="use-azureclient-with-azure-fluid-relay"></a>Azure Fluid Relay で AzureClient を使用する

これは Teams タブ アプリケーションであるため、コラボレーションと対話が主な焦点です。 前に提供したローカル モード `AzureClientProps` を Azure サービス インスタンスの非ローカル資格情報に置き換えて、他のユーザーがアプリケーションに参加して対話できるようにします。 [Azure Fluid Relay サービスをプロビジョニングする方法について説明します](/azure/azure-fluid-relay/how-tos/provision-fluid-azure-portal)。

> [!IMPORTANT]
> 渡 `AzureClientProps` す資格情報が誤ってソース管理にコミットされないようにすることが重要です。 Teams プロジェクトには、資格情報を `.env` 環境変数として格納できるファイルが付属しており、ファイル自体は既 `.gitignore`に . Teams で環境変数を使用するには、「環境変数の [設定と取得](#set-and-get-environment-variable)」を参照してください。

> [!WARNING]
> `InsecureTokenProvider` は、アプリケーションをローカルでテストする便利な方法です。 ユーザー認証を処理し、運用環境に [対してセキュリティで保護されたトークン](/azure/azure-fluid-relay/how-tos/connect-fluid-azure-service) を使用するのは、お客様の責任です。

### <a name="set-and-get-environment-variable"></a>環境変数の設定と取得

環境変数を設定し、Teams で取得するには、組み込みの `.env` ファイルを利用できます。 次のコードを使用して、次の `.env`環境変数を設定します。

```
# .env

TENANT_KEY=foobar
```

ファイルの内容を `.env` クライアント側アプリに渡すには、実行時にファイルに `webpack.config.js` アクセスできるように `webpack` 構成する必要があります。 次のコードを使用して、次の環境変数を `.env`追加します。

```js
// webpack,config.js

webpack.EnvironmentPlugin({
    PUBLIC_HOSTNAME: undefined,
    TAB_APP_ID: null,
    TAB_APP_URI: null,
    REACT_APP_TENANT_KEY: JSON.stringify(process.env.TENANT_KEY) // Add environment variable here
}),
```

で環境変数にアクセスできます。 `Util.ts`

```ts
// Util.ts

tokenProvider: new InsecureTokenProvider(JSON.parse(process.env.REACT_APP_TENANT_KEY!), { id: "user" }),
```

> [!TIP]
> コードを変更すると、プロジェクトが自動的に再構築され、アプリケーション サーバーが再読み込みされます。 ただし、コンテナー スキーマに変更を加えた場合は、アプリケーション サーバーを閉じて再起動した場合にのみ有効になります。 これを行うには、コマンド プロンプトに移動し、Ctrl キーを押しながら C キーを 2 回押します。 その後、実行するか、もう一度実行 `gulp serve` します `gulp ngrok-serve` 。

## <a name="see-also"></a>関連項目

- [Azure Fluid Relay のドキュメント](/azure/azure-fluid-relay)

- [Fluid Framework のドキュメント](https://fluidframework.com/docs/)
- [GitHub リポジトリの流動的な例](https://github.com/microsoft/FluidExamples)
