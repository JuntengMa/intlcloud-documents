### 备份空间如何收费？
云数据库 MySQL 会按地域赠送一定额度的免费备份空间，免费备份空间大小为您在对应地域下所有高可用实例 （包括主实例、灾备实例）的存储空间之和。
超出免费额度的备份空间定价，请参见 [云数据库 MySQL 价格计算器](https://buy.cloud.tencent.com/price/cdb/calculator)。

### 如何减少备份空间开销？
- 删除不再使用的手动备份数据（手动备份可在 [MySQL 控制台](https://console.cloud.tencent.com/cdb) 的实例管理页>备份恢复页面进行删除）。 
- 降低非核心业务的数据自动备份频率（可在控制台调整备份周期和备份保留时间，一周至少备份2次）。
>[回档功能](https://intl.cloud.tencent.com/document/product/236/7276) 基于备份周期和备份保留天数内的数据备份 + 日志备份（binlog），缩短自动备份频率和保留天数会影响实例数据的回档功能，请您权衡备份配置。
>
- 缩短非核心业务的数据备份和日志备份保存时间（备份保留时间为7天已经能满足大多数场景需要）。

| 业务场景             | 备份保留时间                                                 |
| -------------------- | ------------------------------------------------------------ |
| 核心业务             | 建议7天 - 732天                                              |
| 非核心、非数据类业务 | 建议7天                                                      |
| 归档业务             | 建议数据备份保留时间设置为7天，根据实际业务需求手动备份数据，用完及时删除 |
| 测试业务             | 建议数据备份保留时间设置为7天，根据实际业务需求手动备份数据，用完及时删除 |

### 如何设置自动备份?
您可在 [MySQL 控制台](https://console.cloud.tencent.com/cdb) 实例的备份恢复页进行设置。
![](https://main.qcloudimg.com/raw/2480edfc305fffa5dd4358141fb0f328.png)

### 如何删除备份数据？
- 自动备份数据无法手动删除。
- 手动备份数据可在 [MySQL 控制台](https://console.cloud.tencent.com/cdb) 实例的备份恢复页手动删除。

### 如何取消备份任务？
运行中的备份任务不可以取消。

### 备份下载慢如何解决？
推荐您在 [MySQL 控制台](https://console.cloud.tencent.com/cdb) 实例的备份恢复页复制下载地址，并登录到云数据库所在 VPC 下的 CVM（Linux 系统） 中，运用 wget 命令进行内网高速下载，更高效。
>wget 命令格式：wget -c '备份文件下载地址' -O 自定义文件名.xb

### 超出备份保留时间的备份还可以下载或还原吗？
到期后的备份集会自动删除，无法进行下载还原。
- 建议您根据需求合理设置备份保留时间，或在 [MySQL 控制台](https://console.cloud.tencent.com/cdb) 下载备份文件至本地。
- 您也可以在控制台通过手动备份实例数据，手动备份会一直保存。
>手动备份亦会占用备份空间，请合理使用备份空间，避免造成额外的费用。

### 数据和日志备份是否可以关闭？
不可以关闭。但可以通过 [MySQL 控制台](https://console.cloud.tencent.com/cdb) 减少备份频率和删除不再使用的手动备份数据来降低备份空间的占用量。

### 为什么无法发起手动备份任务？
请确认下您设置的自动备份任务时间，如果实例正在进行每天的自动备份，则无法发起手动备份。

### 为什么无法进行分库表的逻辑备份和下载？
[备份新版](https://intl.cloud.tencent.com/document/product/236/32340) 升级后，不论是逻辑备份还是物理备份功能都采用了新的压缩算法，故部分下载功能暂时无法使用。您可以通过手动备份里的【逻辑备份】>【指定库表】功能完成分库表的逻辑备份，同时也可以下载已完成的该次备份。

### 为什么下载的备份文件用 tar 解包解压失败？
>新版的备份文件由于采用的全新压缩算法，使用原有 tar 工具无法正常解包解压，需要使用 xbstream 和 qpress 工具解包解压。

1. 下载新版的备份文件后，应该先用 xbstream （xbstream 为 Percona 的一种打包/解包工具）将其解包：
```
xbstream -x < test_import_57_backup_20181114115236.xb 
```
用 xbstream 解包后会得到后缀名为 .qb 的文件，如：test_import_57_backup_20181114115236.sql.qb
2. 解包后还需要使用 qpress 解压备份文件：
```
qpress -d test_import_57_backup_20181114115236.sql.qp
```
解压后得到完整的备份文件，如：test_import_57_backup_20181114115236.sql

### 如何下载 xbstream 和 qpress 的工具？
- xbstream 为 Percona 的 xtrabackup 备份工具下的一个子程序，要使用 xbstream，需要先安装 Percona 的 xtrabackup，可以使用 yum 安装和二进制安装两种方式来安装 xtrabackup。
- [qpress下载地址](http://www.quicklz.com/)，下载之后通过 tar 命令解出 qpress 二进制文件。
具体 xtrabackup 和 qpress 的安装方式请参见 [使用物理备份恢复数据库](https://intl.cloud.tencent.com/document/product/236/31910)。

### 开发者自己如何备份数据？
云数据库 MySQL 实例每天会进行全量备份，开发者也可以采用云数据库提供的多线程快速导入导出工具进行备份，请参见 [备份方式](https://intl.cloud.tencent.com/document/product/236/32340)，或者通过 mysqldump 工具自己备份数据。

### MySQL 如何查看 binlog 日志？
- 控制台下载 binlog 到本地，例如下载到云服务器。
- 使用 mysqlbinlog 命令查看。MySQL 5.6 需要安装3.4或以上版本的 mysqlbinlog 方支持本地服务器查看 binlog。

### 配置 MySQL 同城双备，能够实现两个实例实时数据同步吗？
可通过云数据库 MySQL 控制台购买 [灾备实例](https://intl.cloud.tencent.com/document/product/236/7272) 来实现此需求。

