## <a name="establish-a-secure-tunnel-to-your-tab"></a>タブへのセキュリティで保護されたトンネルを確立する

Microsoft Teamsはクラウドベースの製品であり、HTTPS エンドポイントを使用してタブ コンテンツをクラウドから利用できる必要があります。 Teamsはローカル ホスティングを許可しない。 タブをパブリック URL に発行するか、ローカル ポートをインターネットに接続する URL に公開するプロキシを使用する必要があります。

タブをテストするには [、ngrok を使用します](https://ngrok.com/docs)。 ngrok がコンピューターで実行されている間、サーバーの Web エンドポイントを使用できます。 ngrok の無料版では、ngrok を閉じると、次回起動する URL が異なります。