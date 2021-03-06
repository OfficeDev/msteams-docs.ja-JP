---
title: カスタム 一緒にモード のシーン
description: カスタムの Together Mode シーンを使用する
ms.topic: conceptual
ms.openlocfilehash: 9b65a0ff32c2f895cd0330f49d985ba48369dccf
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335376"
---
# <a name="custom-together-mode-scenes-in-teams"></a>Teams でのカスタム Together モードのシーン

> [!NOTE]
> この機能は現在、パブリック開発者 [プレビューでのみ利用](../resources/dev-preview/developer-preview-intro.md) できます。

カスタム 一緒にモード Microsoft Teamsは、ユーザーを集め、ビデオを有効にすすめ、臨場感のある魅力的な会議環境を提供します。 参加者を 1 つの仮想シーンにデジタル的に組み合わせ、シーン作成者によって設計および固定された事前に決定されたシートにビデオ ストリームを設定します。

> [!VIDEO https://www.youtube-nocookie.com/embed/MGsNmYKgeTA]

カスタムの Together Mode シーンのシーンは、Microsoft Scene studio を使用してシーン開発者によって作成されたアーティファクトです。 考え出されたシーンの設定では、参加者は指定されたシートを持ち、それらのシートにビデオ ストリームがレンダリングされます。

> [!NOTE]
> シーンのみアプリは、このようなアプリの取得エクスペリエンスがシームレスに行なうので、お勧めします。

次のプロセスでは、シーン専用アプリを作成する概要を示します。

:::image type="content" source="../assets/images/apps-in-meetings/create-together-mode-scene-flow.png" alt-text="シーン専用アプリを作成する" border="false":::

> [!NOTE]
> * シーンのみアプリは、アプリ内のアプリMicrosoft Teams。 Scene studio は、バックグラウンドでアプリ パッケージの作成を処理します。
> * 1 つのアプリ パッケージ内の複数のシーンは、ユーザーに対してフラット なシーンの一覧として表示されます。

## <a name="prerequisites"></a>前提条件

カスタムの Together Mode シーンを使用するには、次の基本的な知識が必要です。

* シーン内のシーンとシートの定義。
* Microsoft Developer アカウントを持ち、開発者ポータルと App Studio Microsoft Teams[を](../concepts/build-and-test/teams-developer-portal.md)理解してください。
* [アプリのサイドローディングの概念](../concepts/deploy-and-publish/apps-upload.md)。
* 管理者がカスタム アプリに対するアクセス許可をアップロードし **、** アプリセットアップポリシーと会議ポリシーの一部としてすべてのフィルターを選択する権限を付与します。

## <a name="best-practices"></a>ベスト プラクティス

シーンを構築する前に、シームレスなシーン構築エクスペリエンスを備える次の点を検討してください。

* すべての画像が PNG 形式で表示されます。
* すべてのイメージを組み合わせて最終的なパッケージが 1920x1080 解像度を超えないようにしてください。

    > [!NOTE]
    > 解像度は、1 つの数値です。 これは、シーンを正常に点灯する必要があります。

* シーンの最大サイズが 10 MB である必要があります。
* 各イメージの最大サイズが 5 MB である必要があります。

    > [!NOTE]
    > * シーンは、複数の画像のコレクションです。 制限は、個々のイメージに対してです。
    > * 個々の画像解像度も、数値である必要があります。
  
* イメージが透明 **な場合** は、[透過] チェック ボックスがオンになっていることを確認します。 このチェック ボックスは、画像が選択されている場合に右側のパネルで使用できます。

    > [!NOTE]
    > 重なり合うイメージは、シーン内のイメージ **が** 重なっているかどうかを示すために、透明としてマークする必要があります。

## <a name="build-a-scene-using-the-scene-studio"></a>シーン スタジオを使用してシーンを構築する

Microsoft には、シーンを構築できる Scene スタジオがあります。 これは[、Scenes Editor - 開発者ポータルでTeams使用できます](https://dev.teams.microsoft.com/scenes)。

> [!NOTE]
> このドキュメントは、開発者ポータルの Scene studio をMicrosoft Teamsしています。 App Studio シーン デザイナーでは、インターフェイスと機能はすべて同じです。

シーン スタジオのコンテキスト内のシーンは、次のアイテムを含むアーティファクトです。

* 会議の開催者および会議の発表者用に予約されているシート。

    > [!NOTE]
    > 発表者は、アクティブに共有しているユーザーを参照しない。 会議の役割 [を参照します](https://support.microsoft.com/en-us/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

* 幅と高さを調整できる各参加者のシートとイメージ。

    > [!NOTE]
    > PNG は、サポートされている唯一の形式です。

* すべてのシートと画像の XYZ 座標。
* 1 つのイメージとしてカモフラージュされた画像のコレクション。

シートのサイズは、参加者のビデオ ストリームをレンダリングするキャンバスになります。 次の図は、シーンを構築するアバターとして表される各シートを示しています。

![シーン スタジオ](../assets/images/apps-in-meetings/scene-design-studio.png)

**シーン スタジオを使用してシーンを作成するには**

1. [シーン[エディター] - [開発者ポータルTeams] に移動します](https://dev.teams.microsoft.com/scenes)。

    >[!NOTE]
    > * Scene studio を開く場合は、開発者ポータルのホーム ページにTeamsし、[会議用のカスタム シーン [の作成](https://dev.teams.microsoft.com/home)]**を選択します**。
    > * Scene studio を開く場合は [、Teams Developer Portal](https://dev.teams.microsoft.com/home)のホーム ページに移動し、左側のセクションから [ツール] を選択し、[ツール] セクションから [**シーン** スタジオ]**を選択** します。

1. [シーン **エディター] ページで、[** 新しい **シーンを作成する] を選択します**。

1. [シーン **] ボックス** に、シーンの名前を入力します。

    >[!NOTE]
    > * [閉じる] **を選択** すると、右側のウィンドウを閉じるか再度開くか切り替えます。
    > * ズーム バーを使用してシーンを拡大または縮小して、シーンをより良く表示できます。

1. 次の図に表示される環境にイメージをドラッグ アンド ドロップします。

    >[!NOTE]
    > * イメージを [ 含むSampleScene.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip) ファイル [SampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) ダウンロードできます。
    > * または、[画像の追加] を使用してシーンに背景画像 **を追加することもできます**。

    ![シーンにドラッグする](../assets/images/apps-in-meetings/drag-and-drop-scene.png)

1. 配置したイメージを選択します。

1. 右側のウィンドウで、画像の配置を選択するか、[サイズ変更] スライダーを使用して画像のサイズを調整します。

    ![画像の配置](../assets/images/apps-in-meetings/image-alignment.png)

1. 画像の外側の領域を選択します。

1. 右上隅で、[レイヤー] の下の [ **参加者]** **を選択します**。

1. [参加者数] ボックスからシーンの参加者数を選択し、[追加] を **選択します**。

    >[!NOTE]
    > * シーンが出荷された後、アバターの配置は実際の参加者のビデオ ストリームに置き換えられる。
    > * 参加者の画像をシーンの周りにドラッグし、必要な位置に配置し、サイズ変更矢印を使用してサイズを変更できます。

1. 参加者の画像を選択し、[スポット **の割** り当て] チェック ボックスをオンにして、参加者にスポットを割り当てる。

1. 参加者の **[会議の開催者****] または [発表** 者] の役割を選択します。

    >[!NOTE]
    > 会議では、1 人の参加者に会議開催者の役割を割り当てる必要があります。

    ![スポットの割り当て](../assets/images/apps-in-meetings/assign-spot.png)

1. [**保存] を** 選択し **、[Teams]** を選択して、シーンをすばやくテストMicrosoft Teams。

    >[!NOTE]
    > 作成したシーンを削除するには、トップ バー **の [シーンの** 削除] を選択します。

1. [ビューの **表示] ダイアログ** Teamsで、[プレビュー] を **選択Teams。**
1. 表示されるダイアログ ボックスで、[追加] を **選択します**。

    テスト会議を作成し、カスタムの Together Mode シーンを起動することで、シーンをテストまたはアクセスできます。 詳細については、「Custom [Together Mode scenes をアクティブ化する」を参照してください](#activate-custom-together-mode-scenes)。

    ![カスタムの一緒にモードのシーンを起動する](../assets/images/apps-in-meetings/launchtogethermode.png)

    >[!NOTE]
    > * [プレビュー **] を** 選択すると、Microsoft Teams開発者ポータルの [アプリ] ページで表示できるアプリTeams作成されます。
    > * [プレビュー **] を** 選択すると、アプリ パッケージが自動的に作成され、appmanifest.jsに表示されます。 前に説明したように、これは抽象化されますが、メニューから [アプリ] に移動すると、自動的に作成された **アプリ** パッケージにアクセスできます。
    > * その後、カスタムの Together Mode シーン ギャラリーでシーンを表示できます。

1. 必要に応じて、[保存] ドロップダウンメニューから [共有] を選択して共有可能なリンクを作成し、他のユーザーが使用するシーンを簡単に配布できます。 このリンクを開くと、ユーザーのシーンがインストールされ、使用を開始できます。

1. プレビュー後、アプリの申請の手順に従って、Teamsをアプリとして出荷できます。

    >[!NOTE]
    > この手順では、設計されたシーンに対して、シーン パッケージとは異なるアプリ パッケージが必要です。 自動的に作成されるアプリ パッケージは、開発者センターの [アプリ] セクションTeams表示されます。

1. 必要に応じて、[保存] ドロップダウン メニューから[エクスポート]を選択して、シーン パッケージを取得できます。 シーン .zipファイルがダウンロードされます。

    ![シーンをエクスポートする](../assets/images/apps-in-meetings/build-a-scene.png)

    >[!NOTE]
    > シーン パッケージは、オンscene.jsシーンの構築に使用される PNG アセットで構成されます。 シーン パッケージは、このドキュメントの「サンプル ドキュメント」のセクションで説明scene.js変更を組み込む場合に確認できます。

Z 軸を活用するより複雑なシーンについては、ステップ バイ ステップの開始サンプルで説明します。

## <a name="sample-scenejson"></a>サンプル scene.jsオン

Scene.jsと共にオンに設定すると、シートの正確な位置が示されます。 シーンは、参加者のビデオを入れるビットマップ イメージ、スプライト、長方形で構成されます。 これらのスプライトと参加者ボックスはワールド座標系で定義され、X 軸は右を指し、Y 軸は下向きを指します。 カスタム一緒にモードシーンは、現在の参加者の拡大をサポートしています。 これは、大規模なシーンでの小規模な会議に役立ちます。 スプライトは、世界に配置された静的なビットマップ イメージです。 スプライトの Z 値は、スプライトの位置を決定します。 レンダリングは、Z 値が最も低いスプライトから始まるので、Z 値が高いほどカメラに近くなります。 各参加者は独自のビデオ フィードを持ち、フォアグラウンドのみをレンダリングするためにセグメント化されます。

サンプルに関するscene.jsを次に示します。

```json
{
   "protocolVersion": "1.0",
   "id": "A",
   "autoZoom": true,
   "mirrorParticipants ": true,
   "extent":{
      "left":0.0,
      "top":0.0,
      "width":16.0,
      "height":9.0
   },
   "sprites":[
      {
         "filename":"background.png",
         "cx":8.0,
         "cy":4.5,
         "width":16.0,
         "height":9.0,
         "zOrder":0.0,
   "isAlpha":false
      },
      {
         "filename":"table.png",
         "cx":8.0,
         "cy":7.0,
         "width":12.0,
         "height":4.0,
         "zOrder":3.0,
   "isAlpha":true
      },
      {
         "filename":"row0.png",
         "cx":12.0,
         "cy":15.0,
         "width":8.0,
         "height":4.0,
         "zOrder":2.0,
   "isAlpha":true
      }

   ],
   "participants":[
      {
         "cx":5.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":0
      },
      {
         "cx":11.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":1
      }
   ]
}
```

各シーンには一意の ID と名前があります。 シーン JSON には、シーンに使用されるすべてのアセットに関する情報も含まれる。 各アセットには、X 軸と Y 軸上のファイル名、幅、高さ、位置が含まれる。 同様に、各シートには、シート ID、幅、高さ、X 軸と Y 軸上の位置が含まれる。 座席の順序は自動的に生成され、好みに応じ変更できます。

> [!NOTE]
> 座席の注文番号は、通話に参加するユーザーの順序に対応します。

zOrder は、Z 軸に沿ってイメージとシートを配置する順序を表します。 多くの場合、必要に応じて深さまたはパーティションの感覚を与えます。 詳細については、ステップ バイ ステップの開始サンプルを参照してください。 このサンプルでは、zOrder を活用します。

サンプル モードをオンにscene.js、カスタムの Together Mode シーンをアクティブ化してシーンに参加できます。

## <a name="activate-custom-together-mode-scenes"></a>カスタムの一緒にモードのシーンをアクティブ化する

エンド ユーザーがカスタムの Together Mode シーンのシーンとどのように関わるかについて、エンドツーエンドの情報を取得します。

**シーンを選択し、カスタムの Together Mode シーンをアクティブにするには**

1. 新しいテスト会議を作成します。

    >[!NOTE]
    > シーン スタジオで **[プレビュー** ] を選択すると、シーンはアプリとしてアプリとしてインストールMicrosoft Teams。 これは、開発者がシーン スタジオからシーンをテストおよび試用するモデルです。 シーンがアプリとして出荷された後、ユーザーはシーン ギャラリーにこれらのシーンを表示します。

1. 左上隅 **の [** ギャラリー] ドロップダウンから、[一緒にモード] **を選択します**。 [ **ピッカー]** ダイアログ ボックスが表示され、追加されたシーンを使用できます。

1. [シーン **の変更] を** 選択して、既定のシーンを変更します。

1. [シーン **ギャラリー] で**、会議に使用するシーンを選択します。

1. 必要に応じて、会議の開催者と発表者は、会議 **のすべての** 参加者のシーンを変更できます。

    >[!NOTE]
    > 任意の時点で、会議に同種のシーンを 1 つしか使用できません。 発表者または開催者がシーンを変更すると、すべてのシーンが変更されます。 カスタムの Together Mode シーンの切り替えと切り替えは、個々の参加者に対して行いますが、カスタムの Together Mode シーンでは、すべての参加者が同じシーンを持っています。

1. **[適用]** を選択します。 Teamsアプリをインストールし、シーンを適用します。

## <a name="open-a-custom-together-mode-scenes-scene-package"></a>カスタムの一緒にモードのシーン を開く シーン パッケージ

シーン スタジオから取得したファイル.zipシーン パッケージを他のクリエイターと共有して、シーンをさらに強化できます。 [ **シーンのインポート]** 機能を利用できます。 このツールは、シーン パッケージのラップを解除して、作成者がシーンを構築し続けるのに役立ちます。

![シーンの zip ファイル](../assets/images/apps-in-meetings/scene-zip-file.png)

## <a name="see-also"></a>関連項目

[会議のTeamsアプリ](teams-apps-in-meetings.md)
