## 操作场景
本文介绍如何通过云服务器控制台及云 API 启动关机状态的实例。




## 操作步骤
### 通过控制台开机实例
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/)。
2. 根据实际需求，选择不同的操作方式。
	- **开机单个实例**：选择需要启动的实例，并在右侧操作栏中，单击【更多】>【实例状态】>【开机】。如下图所示：
![](https://main.qcloudimg.com/raw/5adf1eaf69be183707a56c60991bb73f.png)
	- **开机多个实例**：勾选所有需要开机的实例，在列表顶部，单击【开机】，即可批量开机实例。如下图所示：
![](https://main.qcloudimg.com/raw/e4514bfc1e524e353737414d018a575b.png)

### 通过 API 开机实例
请参考 [StartInstances](https://intl.cloud.tencent.com/document/product/213/33236) 接口。

## 后续操作
只有在实例开机状态时，您才能进行以下操作：
- **登录实例**：根据实例的操作系统，[登录 Linux 实例](https://intl.cloud.tencent.com/document/product/213/5436) 或 [登录 Windows 实例](https://intl.cloud.tencent.com/document/product/213/5435)。
- **[初始化云硬盘](https://intl.cloud.tencent.com/document/product/362/31596)**：对已挂载的云硬盘进行格式化、分区及创建文件系统等初始化操作。
