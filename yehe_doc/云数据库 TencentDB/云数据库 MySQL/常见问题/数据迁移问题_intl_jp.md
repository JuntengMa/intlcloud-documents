### どうやってローカルのSQLファイルをMySQLデータベースにインポートしますか。
>クラウドデータベースMySQLの高可用性バージョンとファイナンス版は、ログ操作管理機能をサポートしています。
>
1. [クラウドデータベースMySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンス名をクリックし管理画面に進みます。
2. 【データベース管理】≻【データベースリスト】≻【データのインポート】を選択し、インポートファイルを選択してから、ターゲットのデータベースを選択して最後にインポートを確定します。
>インポートした1つのSQLファイルは2GB以下で、ファイル名は英字、数字、下線のみ認められています。
>
![](https://main.qcloudimg.com/raw/a8854e74caebb9c69d831dc1583c10c0.png)

### データベースのデータをどうやってエクスポートしますか。
- バックアップデータをエクスポートする際は、[コンソール](https://console.cloud.tencent.com/cdb)でインスタンス名をクリックして管理画面に入り、【バックアップ復旧】画面を選んでダウンロードを行います。
- リアルタイムデータをエクスポートする際は、[読み取り専用インスタンス](https://intl.cloud.tencent.com/document/product/236/7270)を購入し、インスタンスに接続後、mysqldumpツールによってリアルタイムデータを取得できます。

### 元のデータベースは約7GBですが、どの方式が最も速くクラウドデータベースMySQLにマイグレーションできますか。
[データマイグレーション](https://intl.cloud.tencent.com/document/product/571/34103)機能を使用することをお勧めします。お客様の元のデータベースに直接接続しデータの同期を取ることができます。

### 同じ都市で2台の配置を考えていますが、2つのインスタンスでリアルタイムデータの同期が取れますか。
コンソールで[災害復旧インスタンス](https://intl.cloud.tencent.com/document/product/236/7272)を購入すれば、そのニーズは実現できます。


