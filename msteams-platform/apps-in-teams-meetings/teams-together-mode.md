---
title: カスタム Together モードのシーン
description: カスタム Together モードシーンを操作する
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 047e2aa04bfb0196ab7a01e91ce54b01d61f64bf
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2022
ms.locfileid: "64736869"
---
# <a name="custom-together-mode-scenes-in-teams"></a>Teams でのカスタム Together モードのシーン

Microsoft Teams の Custom Together モードシーンは、次のアクションを使用して、イマーシブで魅力的な会議環境を提供します。

* ユーザーを集め、ビデオをオンにするよう促します。
* 参加者を 1 つの仮想シーンにデジタルで結合します。
* 参加者のビデオ ストリームを、シーン作成者によって設計および固定された事前に決定されたシートに配置します。

カスタム Together モードシーンでは、シーンは成果物です。 シーンは、Microsoft Scene Studio を使用してシーン開発者によって作成されます。 想像されたシーンの設定では、参加者はビデオ ストリームを持つシートを持っています。 ビデオは、これらのシートにレンダリングされます。 このようなアプリのエクスペリエンスが明確であるため、シーン専用のアプリをお勧めします。

次のプロセスでは、シーン専用のアプリを作成する概要を示します。

:::image type="content" source="../assets/images/apps-in-meetings/create-together-mode-scene-flow.png" alt-text="シーン専用アプリを作成する" border="false":::

シーン専用のアプリは、Microsoft Teams のアプリのままです。 Scene Studio は、バックグラウンドでアプリ パッケージの作成を処理します。 1 つのアプリ パッケージ内の複数のシーンが、ユーザーに対してフラット リストとして表示されます。

> [!NOTE]
> ユーザーはモバイルから Together モードを開始できません。ただし、ユーザーがモバイル経由で会議に参加し、デスクトップから Together モードを有効にすると、ビデオをオンにしたモバイル ユーザーはデスクトップの Together モードで表示されます。

## <a name="prerequisites"></a>前提条件

カスタムの Together モードシーンを使用するには、次の基本的な知識が必要です。

* シーン内のシーンとシートを定義します。
* Microsoft デベロッパー アカウントを持ち、Microsoft Teams [開発者ポータル](../concepts/build-and-test/teams-developer-portal.md) と App Studio について理解を深めます。
* [アプリサイドローディングの概念](../concepts/deploy-and-publish/apps-upload.md)について説明します。
* 管理者が [**カスタム アプリ**](../concepts/deploy-and-publish/apps-upload.md)をアップロードするアクセス許可を付与していることを確認し、アプリのセットアップポリシーと会議ポリシーの一部としてすべてのフィルターをそれぞれ選択します。

## <a name="best-practices"></a>ベスト プラクティス

シーン構築エクスペリエンスの次のプラクティスを検討してください。

* すべての画像が PNG 形式であることを確認します。
* すべてのイメージがまとめられている最終的なパッケージが 1920 x 1080 の解像度を超えないようにしてください。 解像度は偶数です。 この解像度は、シーンを正常に表示するための必要条件です。
* シーンの最大サイズが 10 MB であることを確認します。
* 各イメージの最大サイズが 5 MB であることを確認します。 シーンは、複数の画像のコレクションです。 制限は、個々の画像に対するものです。
* 必要に応じて [ **透過**] を 選択します。 このチェック ボックスは、画像が選択されている場合に右パネルで使用できます。 重なり合う画像は、シーン内の画像が重複していることを示すために **透過** としてマークする必要があります。

## <a name="build-a-scene-using-the-scene-studio"></a>Scene Studio を使用してシーンを構築する

Microsoft には、シーンを構築できる Scene Studio があります。 これは、 [シーン エディター ( Teams 開発者ポータル) ](https://dev.teams.microsoft.com/scenes)で使用できます。 このドキュメントでは、Microsoft Teams 開発者ポータルの Scene Studio について説明します。 インターフェイスと機能はすべて、App Studio シーン デザイナーで同じです。

Scene Studio のコンテキスト内のシーンは、次の要素を含む成果物です。

* 会議の開催者と会議の発表者用に予約されたシート。 発表者は、アクティブに共有しているユーザーを参照しません。 これは、 [会議の役割](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)を参照します。

* 幅と高さを調整できる各参加者のシートと画像。 画像では PNG 形式のみがサポートされています。

* すべてのシートと画像の XYZ 座標。

* 1 つのイメージとして分離されたイメージのコレクション。

次の図は、シーンを構築するためのアバターとして表される各シートを示しています。

![Scene studio](../assets/images/apps-in-meetings/scene-design-studio.png)

Scene Studio を使用してシーンを構築するには、次の手順を実行します。

1. [シーン エディター - Teams 開発者ポータル](https://dev.teams.microsoft.com/scenes)に移動します。

    または、Scene Studio を開くには、[Teams 開発者ポータル](https://dev.teams.microsoft.com/home)のホーム ページ移動します。
    * **会議のカスタム シーンを作成する** を選択します。
    * 左側のセクションで **Tools** を選択し、[**Tools**] セクションから [**Scene Studio**] を選択します。

1. **シーン エディター** で、**新しいシーンを作成する** を選択します。

1. **シーン名** に、シーンの名前を入力します。

    * **閉じる** を選択すると、右側のウィンドウを閉じるか、もう一度開くかを切り替えることができます。
    * ズーム バーを使用してシーンを拡大または縮小すると、シーンを見やすくすることができます。

1. **イメージの追加** 選択して、環境にイメージを追加します。

    ![環境に画像を追加する](../assets/images/apps-in-meetings/addimages.png)

    >[!NOTE]
    >[SampleScene.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip)をダウンロードし、[SampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) ファイルをイメージと一緒にできます。

1. 追加したイメージを選択します。

1. 右側のウィンドウで、画像の配置を選択するか、 **サイズ変更** を使用して画像のサイズを調整します。

    ![画像の配置](../assets/images/apps-in-meetings/image-alignment.png)

1. 画像の外側の領域を選択します。

1. 右上隅の **レイヤー** の下にある **参加者** を選択します。

1. **参加者数** ボックスからシーンの参加者数を選択し、**追加** を選択します。 シーンが出荷されると、アバターの配置は実際の参加者のビデオ ストリームに置き換えられます。 参加者の画像をシーンの周囲にドラッグし、必要な位置に配置できます。 サイズ変更矢印を使用してサイズを変更できます。

1. 参加者の画像を選択し、[**スポットを割り当てる**] を選択して、参加者にスポットを割り当てます。

1. 参加者の[**会議の開催者**] または [**発表者**] の役割を選択します。 会議では、1 人の参加者に会議開催者の役割を割り当てる必要があります。

    ![スポットの割り当て](../assets/images/apps-in-meetings/assign-spot.png)

1. [**保存**] を選択し、[**Teamsで表示**] を選択して、Microsoft Teams でシーンをすばやくテストします。

    * Teamsで [**表示**] を選択すると、Teams 開発者ポータルの [**アプリ**] ページで表示できる Microsoft Teams アプリが自動的に作成されます。
    * **Teamsで見る** を選択すると、シーンの背後に appmanifest.json であるアプリ パッケージが自動的に作成されます。 メニューから  **Apps** に移動し、自動的に作成されたアプリ パッケージにアクセスできます。
    * 作成したシーンを削除するには、上部のバー **シーン を削除する**] を選択します。

1.  [**Teamsで見る**] で、[**Teamsでプレビュー**] を選択します。
1. 表示されるダイアログ ボックスで、[**追加**] を選択します。

    このシーンは、テスト会議を作成しカスタムの Together Mode シーンを起動することで、テストまたはアクセスされます。 詳細については、「 [カスタム Together Mode シーンをアクティブ化する](#activate-custom-together-mode-scenes)」を参照してください。

    ![カスタム Together モード のシーンを起動する](../assets/images/apps-in-meetings/launchtogethermode.png)

    その後、カスタムの Together Mode シーン ギャラリーでシーンを表示できます。

必要に応じて、[**保存**] ドロップダウン メニューから [**共有**] を選択できます。 共有可能なリンクを作成して、他のユーザーが使用できるようにシーンを配布できます。 ユーザーはリンクを開いてシーンをインストールし、使用を開始できます。

プレビューの後、アプリの申請手順に従って、シーンがアプリとして Teams に配布されます。 この手順では、アプリ パッケージが必要です。 アプリ パッケージは、設計されたシーンのシーン パッケージとは異なります。 自動的に作成されたアプリ パッケージは、Teams デベロッパー センターの **Apps** セクションにあります。

必要に応じて、**保存**]ドロップダウン メニューから **エクスポート** を選択して、シーン パッケージを取得します。 シーン パッケージ .zip ファイルがダウンロードされます。 シーン パッケージには、scene.json と、シーンの構築に使用される PNG アセットが含まれています。 シーン パッケージは、他の変更を組み込むかどうかを確認します。

![シーンをエクスポートする](../assets/images/apps-in-meetings/build-a-scene.png)

Z 軸を使用する複雑なシーンは、ステップ バイ ステップの概要サンプルで示されています。

## <a name="sample-scenejson"></a>サンプル scene.json

Scene.json と画像は、シートの正確な位置を示します。 シーンは、参加者のビデオを配置するビットマップ画像、スプライト、四角形で構成されます。 これらのスプライトと参加者ボックスは、ワールド座標系で定義されます。 X 軸は右を指し、Y 軸は下向きを指します。

Custom Together Mode シーンでは、現在の参加者の拡大表示がサポートされます。 この機能は、大規模なシーンでの小規模な会議に役立ちます。 スプライトは、ワールドに配置された静的ビットマップ イメージです。 スプライトの Z 値によって、スプライトの位置が決まります。 レンダリングは Z 値が最も小さいスプライトで始まるので、Z 値が大きいほどカメラに近いことを意味します。 各参加者には独自のビデオ フィードがあり、前景のみがレンダリングされるようにセグメント化されます。

次のコードは、scene.json サンプルです。

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

各シーンには一意の ID と名前があります。 シーン JSON には、シーンに使用されるすべてのアセットに関する情報も含まれています。 各アセットには、ファイル名、幅、高さ、X 軸と Y 軸上の位置が含まれます。 同様に、各シートには、シート ID、幅、高さ、X 軸と Y 軸上の位置が含まれます。 順序は自動的に生成され、優先順位に従って変更されます。 順序は、通話に参加するユーザーの順序に対応します。

`zOrder`は、画像とシートを Z 軸に沿って配置する順序を表します。 必要に応じて、深さまたはパーティションの感覚を与えます。 ステップ バイ ステップの概要のサンプルを参照してください。 このサンプルでは、 `zOrder`を使用します。

サンプルの scene.json を確認したので、カスタム Together Mode シーンをアクティブ化してシーンに参加できます。

## <a name="activate-custom-together-mode-scenes"></a>カスタム Together モード シーンをアクティブ化する

ユーザーがカスタム Together Mode シーンでシーンを操作する方法について詳しく説明します。

シーンを選択し、カスタムの Together Mode シーンをアクティブ化するには、次の手順を実行します。

1. 新しいテスト会議を作成します。

    >[!NOTE]
    > Scene Studio **プレビュー** を選択すると、シーンは Microsoft Teams にアプリとしてインストールされます。 これは、開発者が Scene Studio からシーンをテストして試すモデルです。 シーンがアプリとして出荷されると、ユーザーはこれらのシーンをシーン ギャラリーに表示します。

1. 左上隅にある **ギャラリー** ドロップダウンから、[ **Together Mode]** を選択します。 [ **ピッカー** ] ダイアログ ボックスが表示され、追加されたシーンを使用できます。

1. [**シーン の変更**] を 選択して、既定のシーンを変更します。

1. **シーン ギャラリー** から、会議に使用するシーンを選択します。

    必要に応じて、会議の開催者と発表者は、会議の **すべての参加者のシーンの変更** ができます。

    >[!NOTE]
    > 任意の時点で、会議に同種のシーンが 1 つだけ使用されます。 発表者または開催者がシーンを変更すると、すべて変更されます。 カスタム Together Mode シーンの切り替えは個々の参加者に対して行われますが、カスタムの Together Mode シーンでは、すべての参加者が同じシーンを持っています。

1. **[適用]** を選択します。Teams はユーザー用のアプリをインストールし、シーンを適用します。

## <a name="open-a-custom-together-mode-scenes-scene-package"></a>カスタム Together Mode シーン パッケージを開く

Scene Studio から取得した .zip ファイルであるシーン パッケージを他の作成者と共有して、シーンをさらに強化できます。 **シーンのインポート** 機能を使用すると、シーン パッケージのラップを解除して、作成者がシーンの構築を続行できるようになります。

![シーンの zip ファイル](../assets/images/apps-in-meetings/scene-zip-file.png)

## <a name="see-also"></a>関連項目

* [Teams 会議用アプリ](teams-apps-in-meetings.md)
* [通話と会議のボット](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
* [Microsoft Teamsでのリアルタイムのメディア通話と会議](~/bots/calls-and-meetings/real-time-media-concepts.md)
