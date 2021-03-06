### MySQLがデータを誤って削除した場合、どのように回復しますか。
- ロールバックによりデータを回復することができます。MySQLはデータベースまたはテーブルをバックアップ周期内の任意の時点にロールバックすることをサポートしています。詳細については、[データのロールバック](https://intl.cloud.tencent.com/document/product/236/7276)をご参照ください。
- XtraBackupツールを使用し、MySQLの物理バックアップファイルをその他のホスト上の自己構築データベースに回復することができます。詳細については、[物理バックアップを使用してデータベースの回復](https://intl.cloud.tencent.com/document/product/236/31910)をご参照ください。
- XtraBackupツールを使用し、MySQLの論理バックアップファイルをその他のホスト上の自己構築データベースに回復することができます。詳細については、[論理バックアップを使用してデータベースの回復](https://intl.cloud.tencent.com/document/product/236/31909)をご参照ください。

### MySQLがデータベースまたはテーブルを誤って削除した場合、どのように回復しますか。
ロールバックによりデータを回復することができます。MySQLはデータベースまたはテーブルをバックアップ周期内の任意の時点にロールバックすることをサポートしています。詳細については、[データのロールバック](https://intl.cloud.tencent.com/document/product/236/7276)をご参照ください。
>ロールバックする必要のあるデータベースまたはテーブルが既に削除されている場合は、先にTencentDBインスタンスにログインし、以前と同じ名称のデータベースまたはテーブルを作成してから、コンソールでロールバックを行う必要があります。

### MySQLが特定の保存を実行する過程で一部の未バックアップデータを削除した場合、データを復元できますか。
コンソールのロールバック機能を使用して、バックアップ周期内の任意の時点のデータを復元することができます。

### MySQLのロールバック時に、現在のテーブルデータは上書きされますか。
ロールバック操作により、新しいデータベースまたはテーブルが元のインスタンスに生成されます。ロールバックが完了後、元のデータベースまたはテーブル、および新規作成されたデータベースまたはテーブルを見ることができます。ロールバック後の新しいデータベースまたはテーブルの名前は、元のデータベースまたはテーブル名_bakです。

### MySQLのロールバックの過程で、どのようにロールバックの進行状況とログをリアルタイムにクエリしますか。
ロールバックの過程で、ロールバックの進行状況とログをリアルタイムにクエリすることができます。[データのロールバック](https://intl.cloud.tencent.com/document/product/236/7276)をご参照ください。

