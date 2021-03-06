## 开发模式
Serverless Framework CLI 支持开发模式（dev 模式），处于开发状态下的项目可以更便捷的进行代码编写及开发调试。在开发模式中，用户可以持续地进行开发 - 调试的过程，减少了打包、更新等其他工作的干扰。
<span id="joinDev"></span>
### 进入开发模式
在项目下执行 `serverless dev` 命令，可以进入项目的开发模式。示例如下：
>目前 `serverless dev`  仅支持 Node.js 10.15 及 12.16 运行环境。
>
```
$ serverless dev
serverless ⚡ framework
Dev Mode - Watching your Component for changes and enabling streaming logs, if supported...
Debugging listening on ws://127.0.0.1:9222.
For help see https://nodejs.org/en/docs/inspector.
Please open chorme, and visit chrome://inspect, click [Open dedicated DevTools for Node] to debug your code.
--------------------- The realtime log ---------------------
17:13:38 - express-api-demo - deployment
region: ap-guangzhou
apigw:
  serviceId:   service-b77xtixx
  subDomain:   service-b77xtixx-12539702xx.gz.apigw.tencentcs.com
  environment: release
  url:         http://service-b77xtixx-12539702xx.gz.apigw.tencentcs.com/release/
scf:
  functionName: express_component_6r6xkh60k
  runtime:      Nodejs10.15
  namespace:    default
express-api-demo › Watching
```
在进入 dev 模式后，Serverless 工具将输出部署的内容，并启动持续文件监控。当代码文件有更新时，将自动再次进行部署，将本地文件更新到云端。



### 退出开发模式
在开发模式下，可通过 `Ctrl+C` 退出。返回结果如下所示：
```
express-api-demo › Disabling Dev Mode & Closing ...
express-api-demo › Dev Mode Closed
```


## 云端调试

Runtime 为 Node.js 10+ 的项目，可开启云端调试，使用调试工具来连接远程环境并进行调试。例如，Chrome DevTools、VS Code Debugger。

### 使用须知及注意事项
当前云函数的云端调试能力处于 Beta 阶段，欢迎试用并向我们反馈使用中的问题或建议。
在使用云函数的云端调试时，需要先了解如下信息或注意点：

- 云端调试是使用了云函数的一个实际运行实例来进行调试。
- 由于触发事件的随机性，如果有多个实例存在的情况下，触发事件可能随机的落到某个实例上，因此不是任意请求均能命中调试实例并开始调试。
- 调试断点暂停运行时：
	- 长时间未运行且无返回的情况下，可能会导致触发端例如 API 网关提示超时。
	- 实例仍将处于计时状态，并在此次调试完成后，持续运行到执行完成时，记录耗费的总时长作为此次函数的运行时长。
- 从触发实例运行到最终完成调试，单次执行完成的最长时间为900s。若在调试时中断执行900s后，将会强制终止此次执行，并按照函数运行时间900s进行统计和计量。
- 目前版本的调试能力，会使云函数超时配置为900s，在正常退出调试时将会重新设置超时为正常值。如果强行终止调试或异常退出，会导致云函数超时未能设置为正常值，此时可以通过再次部署（命令行）或手工编辑（控制台）的方式调整云函数的超时配置。



### 开启云端调试
执行步骤 [进入开发模式](#joinDev) 时，如果项目是 Runtime 为 Node.js 10及以上版本的函数，会自行开启云端调试，并输出调试相关信息。
例如，在开启开发模式时，输出结果包含类似如下信息，则代表已经启动该项目的云端调试：
```plaintext
Debugging listening on ws://127.0.0.1:9222.
For help see https://nodejs.org/en/docs/inspector.
Please open chorme, and visit chrome://inspect, click [Open dedicated DevTools for Node] to debug your code.
```

### 使用调试工具 Chrome DevTools
以下步骤说明如何使用 Chrome 浏览器的 DevTools 工具来连接远程环境并进行调试：
1. 启动 Chrome 浏览器。
2. 在地址栏中输入 `chrome://inspect/` 并访问。
3. 可通过以下两种方式打开 DevTools。如下图所示：
![](https://main.qcloudimg.com/raw/a731827f731370cce0a245ef7252e4ea.png)
 1. （推荐）单击 Devices 下的【Open dedicated DevTools for Node】。
 2. 选择 Remote Target #LOCALHOST 中具体 Target 下的【inspect】。
如果无法打开或者没有 Target，请检查 Device 的 Configure 中是否已有 `localhost:9229` 或 `localhost:9222` 的配置，该配置对应开启云端调试时的输出。
4. 通过选择【Open dedicated DevTools for Node】方式打开的 DevTools 调试工具，可单击【Sources】页签看远端代码。函数的实际代码在 `/var/user/` 目录下。
在【Sources】页签中查看的代码可能处于加载中，会随着调试进行而展示出更多远端文件。
5. 可按需打开文件，在文件的指定位置设置断点。
6. 通过任意方式，例如 URL 访问、页面触发、命令触发、接口触发等方式触发函数，会使得远端环境开始运行，并会在设置了断点的位置中断，等待进一步的运行。
8. 通过 DevTools 的右侧工具栏，可以控制中断的程序继续执行、单步执行、步入步出等操作，也可以直接查看当前变量，或设定需跟踪查看的变量。DevTools 的进一步使用可以搜索查询 DevTools 使用说明文档。

### 关闭云端调试

在退出开发模式时，将会自动关闭云端调试功能。
