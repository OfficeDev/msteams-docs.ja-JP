---
title: メディア機能を統合する
author: Rajeshwari-v
description: Teams JavaScript クライアント SDK を使用して、コード例を使用してメディア機能を有効にする方法と、メディア機能を統合する利点についても説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: bfa63b42383e507f004b0225c64f381e47e547f0
ms.sourcegitcommit: 1ea035bc20303070268db38472839584ad4280b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2022
ms.locfileid: "68653372"
---
# <a name="integrate-media-capabilities"></a>メディア機能を統合する

カメラやマイクなどのネイティブ デバイス機能を Teams アプリと統合できます。 統合には、アプリがユーザーの[デバイスアクセス許可](native-device-permissions.md)にアクセスするために必要なツールを提供する [Microsoft Teams JavaScript クライアント SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) を使用できます。 適切なメディア機能 API を使用して、カメラやマイクなどのデバイス機能を Microsoft Teams アプリ内の Teams プラットフォームと統合し、より豊富なエクスペリエンスを構築します。 メディア機能は、Teams Web クライアント、デスクトップ、モバイルで使用できます。 メディア機能を統合するには、アプリ マニフェスト ファイルを更新し、メディア機能 API を呼び出す必要があります。

効果的な統合を実現するには、ネイティブ メディア機能を使用できる、それぞれの API を呼び出すための [コード スニペット](#code-snippets) を十分に理解している必要があります。 Teams アプリのエラーを処理するには、[API 応答エラー](#error-handling)を理解しておくことが重要です。

## <a name="advantages"></a>メリット

デバイス機能を Teams アプリに統合する利点は、ネイティブ Teams コントロールを使用して、ユーザーに豊富でイマーシブなエクスペリエンスを提供できることです。 次のシナリオでは、メディア機能の利点を示します。

* ユーザーが携帯電話で物理ホワイトボードに描画された大まかなモックアップをキャプチャし、キャプチャした画像を Teams グループ チャットの投票オプションとして使用できるようにします。

* ユーザーがオーディオ メッセージを録音し、インシデント チケットに添付できるようにします。

* ユーザーがスマートフォンから物理的なドキュメントをスキャンして自動車保険金請求を提出できるようにします。

* ユーザーが職場でビデオを録画し、出席のためにアップロードできるようにします。

> [!NOTE]
>
> * 現時点では、Teams では、ポップアップ チャット ウィンドウ、タブ、会議サイド パネルでのデバイスアクセス許可はサポートされていません。</br>
> * デバイスのアクセス許可はブラウザーで異なります。 詳細については、「[ブラウザー デバイスのアクセス許可](browser-device-permissions.md)」を参照してください。
> * 関連する Teams API が開始されると、要求のアクセス許可プロンプトがモバイルに自動的に表示されます。 詳細については、「[デバイスのアクセス許可要求](native-device-permissions.md)」 を参照してください。

## <a name="update-manifest"></a>マニフェストを更新する

`devicePermissions` プロパティを追加して `media` を指定することにより、Teamsアプリの [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) ファイルを更新します。 これにより、アプリは、 カメラ を使用して画像をキャプチャする前にユーザーに必要なアクセス許可を要求したり、ギャラリーを開いて添付ファイルとして送信する画像を選択したり、 マイク を使用して会話を記録したりできます。 アプリ マニフェストの更新プログラムは次のとおりです。

``` json
"devicePermissions": [
    "media",
],
```

## <a name="media-capability-apis"></a>メディア機能 API

[selectMedia](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia)、[getMedia](/javascript/api/@microsoft/teams-js/media.media#@microsoft-teams-js-media-media-getmedia)、[viewImages](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-viewimages) API を使用すると、ネイティブ メディア機能を次のように使用できます。

* ネイティブ **マイク** を使用して、ユーザーがデバイスから **オーディオを録音** (10 分間の会話を録音) できるようにします。
* ネイティブ **カメラ コントロール** を使用して、ユーザーが外出先で **画像をキャプチャして添付** し、 **ビデオをキャプチャ** (最大 5 分間のビデオを記録) できるようにします。
* ネイティブ **ギャラリーのサポート** を使用して、ユーザーが添付ファイルとして **デバイス イメージを選択** できるようにします。
* ネイティブ **イメージ ビューアー コントロール** を使用して、一度に **複数のイメージをプレビュー** します。
* SDK ブリッジを介した **大規模なイメージ転送** (1 MB から 50 MB) をサポートします。
* ユーザー **が画像を** プレビューおよび編集できるようにすることで、高度なイメージ機能をサポートします。
* カメラを使用してドキュメント、ホワイトボード、名刺をスキャンします。
  
> [!IMPORTANT]
>
> * `selectMedia`、`getMedia`、および `viewImages` API は、タスク モジュール、タブ、個人用アプリなど、複数の Teams サーフェスから呼び出すことができます。 詳細については、「 [Teams アプリのエントリ ポイント」を](../extensibility-points.md)参照してください。</br>
> * API は `selectMedia` 、さまざまな入力構成を通じてカメラとマイクの両方の機能をサポートします。
> * マイク機能にアクセスするための API は `selectMedia` 、モバイル クライアントでのみサポートされます。
> * アップロードされるイメージの最大数は、API によって [`maxMediaCount`](/javascript/api/@microsoft/teams-js/media.mediainputs#@microsoft-teams-js-media-mediainputs-maxmediacount) 返される配列の合計サイズによっても `selectMedia` 決まります。 配列サイズが 4 MB を超える場合は、配列サイズが 4 MB を超えていないことを確認します。API によってエラー コード 10000 が生成され、エラーがSIZE_EXCEEDEDされます。

次の表に、デバイスのメディア機能を有効にする API のセットを示します。

| API      | 説明   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia) (**カメラ)**| この API を使用すると、ユーザーは **デバイス カメラからメディアをキャプチャまたは選択** し、それを Web アプリに返すことができます。 ユーザーは、送信前に画像の編集、トリミング、回転、注釈付け、または描画を行うことができます。 `selectMedia` に対応して、Web アプリは、選択した画像のメディア ID と、選択したメディアのサムネイルを受信します。 この API は、 [ImageProps](/javascript/api/@microsoft/teams-js/media.imageprops) 構成を使用してさらに構成できます。 |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-selectmedia) (**マイク**)| マイク機能にアクセスするための API で `selectMedia` [mediaType](/javascript/api/@microsoft/teams-js/media.mediatype) を `4` (Audio) に設定します。 この API を使用すると、ユーザーはデバイスマイクからオーディオを録音し、記録されたクリップを Web アプリに返すこともできます。 ユーザーは、送信前に記録プレビューを一時停止、再記録、再生できます。  **selectMedia** に応答して、Web アプリは選択したオーディオ録音のメディア ID を受信します。 <br/> 会話を記録するための期間を分単位で構成する必要がある場合は、使用 `maxDuration`します。 現在の記録時間は 10 分です。その後、記録は終了します。  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/media.media#@microsoft-teams-js-media-media-getmedia)| この API は、メディア サイズに関係なく、`selectMedia` API によってキャプチャされたメディアをチャンク単位で取得します。 これらのチャンクは、ファイルまたは BLOB として組み立てられ、Web アプリに送り返されます。 メディアを小さなチャンクに分割すると、大きなファイル転送が容易になります。 |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media#@microsoft-teams-js-media-viewimages)| この API を使用すると、ユーザーはスクロール可能なリストとして全画面表示モードで画像を表示できます。|

# <a name="mobile"></a>[モバイル](#tab/mobile)

次の図は、イメージ機能に対する API の `selectMedia` Web アプリ エクスペリエンスを示しています。

:::image type="content" source="~/assets/images/tabs/media-capability-mobile2.png" alt-text="図は、モバイルの画像機能を示しています。":::

> [!NOTE]
> Android バージョンが 7 未満のデバイスでは、ネイティブ Teams カメラ エクスペリエンスではなく、 `selectMedia` ネイティブ Android カメラ エクスペリエンスが API によって起動されます。

次の図は、マイク機能に対する API の Web アプリ エクスペリエンス `selectMedia` を示しています。

:::image type="content" source="~/assets/images/tabs/microphone-capability.png" alt-text="図は、モバイルのマイク機能を示しています。":::

# <a name="desktop"></a>[デスクトップ](#tab/desktop)

次の図は、イメージ機能に対する API の `selectMedia` Web アプリ エクスペリエンスを示しています。

:::image type="content" source="~/assets/images/tabs/media-capability-desktop1.png" alt-text="図は、デスクトップのメディア機能を示しています。":::

---

## <a name="error-handling"></a>エラー処理

Teams アプリでこれらのエラーを適切に処理してください。 次の表に、エラー コードとエラーが生成される説明を示します。

|エラー コード |  エラー名     | 説明|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | API は現在のプラットフォームではサポートされていません。|
| **404** | FileNotFound | 指定されたファイルが指定された場所に見つかりません。|
| **500** | 内部エラーです(_E) | 必要な操作の実行中に内部エラーが発生しました。|
| **1000** | PERMISSION_DENIED |アクセス許可がユーザーによって拒否されました。|
| **3000** | NO_HW_SUPPORT | ハードウェアは機能をサポートしていません。|
| **4000**| 引数が無効です | いくつかの引数は無効です。|
|  **8000** | USER_ABORT |ユーザーが操作を中止します。|
| **9000**| OLD_PLATFORM | プラットフォーム コードは古く、この API は実装されていません。|
| **10,000**| SIZE_EXCEEDED |  戻り値が大きすぎて、プラットフォーム サイズの境界を超えています。|

## <a name="code-snippets"></a>コード スニペット

* カメラを使用して画像をキャプチャするための API を呼び出します `selectMedia` 。

    ```javascript
    let imageProp: microsoftTeams.media.ImageProps = {
        sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
        startMode: microsoftTeams.media.CameraStartMode.Photo,
        ink: false,
        cameraSwitcher: false,
        textSticker: false,
        enableFilter: true,
    };
    let mediaInput: microsoftTeams.media.MediaInputs = {
        mediaType: microsoftTeams.media.MediaType.Image,
        maxMediaCount: 10,
        imageProps: imageProp
    };
    microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
        if (error) {
            if (error.message) {
                alert(" ErrorCode: " + error.errorCode + error.message);
            } else {
                alert(" ErrorCode: " + error.errorCode);
            }
        }
        if (attachments) {
            let y = attachments[0];
            img.src = ("data:" + y.mimeType + ";base64," + y.preview);
        }
    });
    ```

* カメラを使用してビデオをキャプチャするための API を呼び出します `selectMedia` 。

  * 次を使用してビデオをキャプチャする `fullscreen: true`:

       `fullscreen: true` は、ビデオ記録モードでカメラを開きます。 前面カメラと背面カメラの両方を使用するオプションが用意されており、次の例で説明されているように他の属性も提供されます。

       ```javascript
        
         const defaultLensVideoProps: microsoftTeams.media.VideoProps = {
             sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
             startMode: microsoftTeams.media.CameraStartMode.Video,
             cameraSwitcher: true,
             maxDuration: 30
        }
         const defaultLensVideoMediaInput: microsoftTeams.media.MediaInputs = {
             mediaType: microsoftTeams.media.MediaType.Video,
             maxMediaCount: 6,
             videoProps: defaultLensVideoProps
        }
       ```

  * 次を使用してビデオをキャプチャする `fullscreen: false`:

       `fullscreen: false` は、ビデオ録画モードでカメラを開き、フロント カメラのみを使用します。 通常 `fullscreen: false` は、ユーザーがデバイス画面でコンテンツを読み取っている間にビデオを記録する場合に使用されます。

       このモードでは `isStopButtonVisible: true` 、ユーザーが記録を停止できるようにする停止ボタンを画面に追加することもできます。 場合 `isStopButtonVisible: false`は、mediaController API を呼び出すか、記録期間が指定された時間に達 `maxDuration` したときに記録を停止できます。

       時刻を指定して記録を停止する例を次に `maxDuration` 示します。

       ```javascript
          const defaultNativeVideoProps: microsoftTeams.media.VideoProps = {
             maxDuration: 30,
             isFullScreenMode: false,
             isStopButtonVisible: false,
             videoController: new microsoftTeams.media.VideoController(videoControllerCallback)
         }
          const defaultNativeVideoMediaInput: microsoftTeams.media.MediaInputs = {
             mediaType: microsoftTeams.media.MediaType.Video,
             maxMediaCount: 1,
             videoProps: defaultNativeVideoProps
         }
       ```

       mediaController API を呼び出して記録を停止する例を次に示します。

       ```javascript
          const defaultNativeVideoProps: microsoftTeams.media.VideoProps = {
             videoController.stop(),
             isFullScreenMode: false,
             isStopButtonVisible: false,
             videoController: new microsoftTeams.media.VideoController(videoControllerCallback)
         }
          const defaultNativeVideoMediaInput: microsoftTeams.media.MediaInputs = {
             mediaType: microsoftTeams.media.MediaType.Video,
             maxMediaCount: 1,
             videoProps: defaultNativeVideoProps
         }
       ```

* カメラを使用して画像とビデオをキャプチャするための API を呼び出 `selectMedia` します。

  これにより、ユーザーは画像またはビデオのキャプチャを選択できます。

    ```javascript
    
      const defaultVideoAndImageProps: microsoftTeams.media.VideoAndImageProps = {
        sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
        startMode: microsoftTeams.media.CameraStartMode.Photo,
        ink: true,
        cameraSwitcher: true,
        textSticker: true,
        enableFilter: true,
        maxDuration: 30
      }
    
      const defaultVideoAndImageMediaInput: microsoftTeams.media.MediaInputs = {
        mediaType: microsoftTeams.media.MediaType.VideoAndImage,
        maxMediaCount: 6,
        videoAndImageProps: defaultVideoAndImageProps
      }
    
      let videoControllerCallback: microsoftTeams.media.VideoControllerCallback = {
        onRecordingStarted() {
          console.log('onRecordingStarted Callback Invoked');
        },
      };
    
      microsoftTeams.media.selectMedia(defaultVideoAndImageMediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
        if (error) {
            if (error.message) {
                alert(" ErrorCode: " + error.errorCode + error.message);
            } else {
                alert(" ErrorCode: " + error.errorCode);
            }
        }
        
        var videoElement = document.createElement("video");
        attachments[0].getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
        if (blob) {
            if (blob.type.includes("video")) {
                videoElement.setAttribute("src", URL.createObjectURL(blob));
            }
        }
        if (error) {
            if (error.message) {
                alert(" ErrorCode: " + error.errorCode + error.message);
            } else {
                alert(" ErrorCode: " + error.errorCode);
            }
        }
        });
        });
        
    ```

* API を呼び出 `getMedia` して、大きなメディアをチャンク単位で取得します。

    ```javascript
    let media: microsoftTeams.media.Media = attachments[0]
    media.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
        if (blob) {
            if (blob.type.includes("image")) {
                img.src = (URL.createObjectURL(blob));
            }
        }
        if (error) {
            if (error.message) {
                alert(" ErrorCode: " + error.errorCode + error.message);
            } else {
                alert(" ErrorCode: " + error.errorCode);
            }
        }
    });
    ```

* API によって返される ID で `selectMedia` API を呼び出します`viewImages`。

    ```javascript
    // View images by id:
    // Assumption: attachmentArray = select Media API Output
    let uriList = [];
    if (attachmentArray && attachmentArray.length > 0) {
        for (let i = 0; i < attachmentArray.length; i++) {
            let file = attachmentArray[i];
            if (file.mimeType.includes("image")) {
                let imageUri = {
                    value: file.content,
                    type: 1,
                }
                uriList.push(imageUri);
            } else {
                alert("File type is not image");
            }
        }
    }
    if (uriList.length > 0) {
        microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
            if (error) {
                if (error.message) {
                    output(" ErrorCode: " + error.errorCode + error.message);
                } else {
                    output(" ErrorCode: " + error.errorCode);
                }
            }
        });
    } else {
        output("Url list is empty");
    }
    ```

* URL で API を呼び出す `viewImages` :

    ```javascript
    // View Images by URL:
    // Assumption 2 urls, url1 and url2
    let uriList = [];
    if (URL1 != null && URL1.length > 0) {
        let imageUri = {
            value: URL1,
            type: 2,
        }
        uriList.push(imageUri);
    }
    if (URL2 != null && URL2.length > 0) {
        let imageUri = {
            value: URL2,
            type: 2,
        }
        uriList.push(imageUri);
    }
    if (uriList.length > 0) {
        microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
            if (error) {
                if (error.message) {
                    output(" ErrorCode: " + error.errorCode + error.message);
                } else {
                    output(" ErrorCode: " + error.errorCode);
                }
            }
        });
    } else {
        output("Url list is empty");
    }
    ```

* マイクを介してオーディオを録音するための通話 `selectMedia` と `getMedia` API:

    ```javascript
      let mediaInput: microsoftTeams.media.MediaInputs = {
        mediaType: microsoftTeams.media.MediaType.Audio,
        maxMediaCount: 1,
        };
        microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
            if (error) {
                if (error.message) {
                    alert(" ErrorCode: " + error.errorCode + error.message);
                } else {
                    alert(" ErrorCode: " + error.errorCode);
                }
            }
        // If you want to directly use the audio file (for smaller file sizes (~4MB))    if (attachments) {
        let audioResult = attachments[0];
        var videoElement = document.createElement("video");
        videoElement.setAttribute("src", ("data:" + audioResult.mimeType + ";base64," + audioResult.preview));
        audioResult.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
        if (blob) {
            if (blob.type.includes("video")) {
                videoElement.setAttribute("src", URL.createObjectURL(blob));
            }
        }
        if (error) {
            if (error.message) {
                alert(" ErrorCode: " + error.errorCode + error.message);
            } else {
                alert(" ErrorCode: " + error.errorCode);
            }
        }
    });
    });
    ```

## <a name="file-download-on-teams-mobile"></a>Teams Mobile でのファイルのダウンロード

ユーザーが Webview からモバイル デバイスにファイルをダウンロードできるようにアプリを構成できます。

>[!NOTE]
> ファイルのダウンロードは Android Teams モバイル クライアントでのみサポートされ、認証されていないファイルのみをダウンロードできます。

有効にするには、次の手順に従います。

1. Teams アプリ [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) ファイルを更新するには、プロパティを`devicePermissions`追加し、[更新マニフェスト](#update-manifest)に示すように指定`media`します。

2. 次の形式を使用し、HMTL ダウンロード属性を Web ページに追加します。

    ```html
    <a href="path_to_file" download="download">Download</a>
    ```

## <a name="see-also"></a>関連項目

* [Teams で QR コードまたはバーコード スキャナー機能を統合する](qr-barcode-scanner-capability.md)
* [Teams で位置情報機能を統合する](location-capability.md)
* [ユーザー ピッカーを統合する](people-picker-capability.md)
* [アプリケーションでホストされるメディア ボットの要件と考察](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
