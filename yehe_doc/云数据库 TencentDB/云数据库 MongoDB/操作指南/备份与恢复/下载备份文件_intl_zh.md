## 获取备份下载链接
>?通过子账号下载备份需先进行账号授权，请参见 [授权子账号下载备份](https://intl.cloud.tencent.com/document/product/240/36356)。

>
1. 登录 [云数据库 MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，在实例列表中，单击实例名进入实例管理页面。
2. 在【备份与回档】>【备份列表】页，单击【下载】，获取备份下载需要的地域码、存储桶、下载地址。
![](https://main.qcloudimg.com/raw/64aabb71efe9e9b297adf628f7351d87.png)

## 配置 COSCMD
1. 登录 [访问管理控制台](https://console.cloud.tencent.com/cam/capi)，在【API密钥管理】页获取 SecretId 和 SecretKey。
2. 下载云数据库 MongoDB 备份文件需要使用的 [COSCMD 工具](https://intl.cloud.tencent.com/document/product/436/10976)。
3. 配置 COSCMD，请参见 [配置参数](https://intl.cloud.tencent.com/document/product/436/10976#.E9.85.8D.E7.BD.AE.E5.8F.82.E6.95.B0)。
例如，获取到的 SecretId 为`IKIDxxxxxxxxxxx20Eb`，SecretKey 为 `TbecxxxxxxxxxxxT4Yw`，地域码为`ap-guangzhou`，存储桶为`mognodb-backup-test-1251937`，则 COSCMD 配置如下：
```
coscmd config -a IKIDxxxxxxxxxxx20Eb -s TbecxxxxxxxxxxxT4Yw -b mognodb-backup-test-1251937 -r ap-guangzhou
```

## 下载备份文件
1. [登录 Linux 云服务器](https://intl.cloud.tencent.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8)，指定一个下载目录（需保证该目录为空），如果没有需要新建一个，命令如下：
```
mkdir dump
```
>!Linux 云服务器的内网地址须在如下任一网段范围内，否则无法下载备份文件。
>- 192.168.0.0/16 
>- 172.16.0.0/16
>- 172.20.0.0/16
>- 172.24.0.0/16
>- 172.27.0.0/16
>- 10.0.0.0/8

2. 执行下载命令，下载链接通过 MongoDB 控制台获取。例如，下载链接为`cmongo_backup/cmgo-pfsumk5l_0/snapshot/1544517026`，则命令如下：
```
coscmd  download -r  cmongo_backup/cmgo-pfsumk5l_0/snapshot/1544517026  dump/
```
>
>- 副本集只有一个下载链接。
>- 分片集群的每个片会有一个下载链接，数据下载时需指定存放在不同的下载目录，防止下载数据被覆盖。
>- 下载时必须加 -r 命令来下载文件夹。
3. 下载完成后可查看下载文件，如下图所示：
![](https://main.qcloudimg.com/raw/163d25eee187b4292261518af8dcd1c1.png)

