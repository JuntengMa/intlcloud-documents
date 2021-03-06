## 购买说明
腾讯云容器镜像服务目前处于免费公测阶段，您可前往 [容器镜像服务控制台](https://console.cloud.tencent.com/tcr) 开始使用。在使用过程中，将涉及使用腾讯云对象存储产品 COS，并根据您的实际使用情况产生相应费用。

公测结束后，本产品将开始商业化计费。正式收费前我们将通过产品发布台、站内信、邮件等渠道进行通知，您可放心使用。


## 支持地域
目前容器镜像服务当前已支持及近期即将支持地域如下表所示：
<table>
<tbody>
<tr>
<th>地域</th><th>取值</th>
</tr>
<tr>
<td>广州</td><td>ap-guangzhou</td>
</tr>

<tr>
<td>上海</td><td>ap-shanghai</td>
</tr>

<tr>
<td>南京（<a href="https://console.cloud.tencent.com/workorder/category">提交工单</a> 申请开通）</td><td>ap-nanjing</td>
</tr>

<tr>
<td>北京</td><td>ap-beijing</td>
</tr>

<tr>
<td>中国香港</td><td>ap-hongkong</td>
</tr>

<tr>
<td>首尔</td><td>ap-seoul</td>
</tr>

<tr>
<td>硅谷</td><td>na-siliconvalley</td>
</tr>

</tbody></table>

## 企业版收费项
<table>
<tr>
<th>项目</th>
<th>说明</th>
<th>价格</th>
</tr>
<tr>
<td>实例租用</td>
<td>企业版实例按照实例规格及所在地域区分不同的价格。</td>
<td>公测期间免费</td>
</tr>
<tr>
<td>存储费用</td>
<td>企业版的云原生应用制品（例如容器镜像、Helm Chart）托管在您的 COS Bucket 中，根据实际使用情况将产生存储和流量的费用。按照 COS 计费方式进行计费，也可前往 <a href="https://console.cloud.tencent.com/expense/overview">费用中心</a> 进行查询。<br><b>注意：</b>使用实例同步功能进行跨地域同步容器镜像及 Helm Chart，不会产生 COS 公网流量费用。</td>
<td>请参见 <a href="https://intl.cloud.tencent.com/document/product/436/6239">COS 定价</a>。</td>
</tr>
<tr>
<td>流量费用</td>
<td>通过公网进行容器镜像及 Helm Chart 上传、下载及跨地域同步操作，将产生流量费用。流量费用对应不同规格具有免费配额及限制，如需提高跨地域数据同步带宽，请 <a href="https://console.cloud.tencent.com/workorder/category">提交工单</a>。</td>
<td>暂不收费，特殊场景请提交工单咨询。</td>
</tr>
</table>


## 容器镜像服务规格
容器镜像服务规格如下，其中 **✓** 代表支持，**-** 代表不支持。

<table>
<tbody><tr>
<th rowspan="2" style="
    width: 13%;
">功能模块</th>
<th rowspan="2" style="
    width: 27%;
">功能特性</th>
<th rowspan="2" style="
    width: 5%;
">个人版</th>
<th colspan="3" style="
    width: 55%;
">企业版</th>
</tr>
<tr>
<th>基础版</th><th>标准版</th><th>高级版</th>
</tr>
<tr>
<td rowspan="3">实例管理</td>
<td>独享 Registry 服务</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>独享服务访问域名</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>独享数据存储后端</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td rowspan="5">仓库管理</td>
<td>多级仓库目录</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>Helm Chart 托管</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>命名空间配额</td><td>10</td><td>50</td><td>100</td><td>500</td>
</tr>
<tr>
<td>镜像仓库配额</td><td>500</td><td>1000</td><td>3000</td><td>5000</td>
</tr>
<tr>
<td>Helm 仓库配额</td><td>-</td><td>1000</td><td>3000</td><td>5000</td>
</tr>
<tr>
<td rowspan="4">安全管控</td>
<td>网络访问控制</td>
<td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>VPC 接入配额</td><td>-</td><td>3</td><td>5</td><td>10</td>
</tr>
<tr>
<td>镜像漏洞扫描</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>操作日志保留</td><td>-</td><td>7天</td><td>15天</td><td>30天</td>
</tr>
<tr>
<td rowspan="2">同步备份</td>
<td>跨实例（地域）自动同步</td>
<td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>同城多可用区容灾</td><td>-</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td rowspan="5">容器 DevOps</td>
</tr>
<tr>
<td>Webhook 触发器类型</td><td>-</td><td>推送<br>镜像</td><td>推送镜像、<br>Helm Chart</td><td>推送/拉取/删除镜像、<br>Helm Chart</td>
</tr>
<tr>
<td>容器镜像编译构建</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>云原生交付工作流</td><td>-</td><td>-</td><td>✓</td><td>✓</td>
</tr>
<tr>
<td>P2P 镜像加速分发</td><td>✓</td><td>✓</td><td>✓</td><td>✓</td>
</tr>
</tbody></table>

#### 公测期间说明事项
- VPC 接入配额公测期间各个规格均限制为1 ，请根据实际需要提交工单申请调整配额。
- 操作日志查询功能暂未开放使用，如有需要，请提交工单申请查询。
- Webhook 触发器类型公测期间无规格限制，仅支持推送及删除两种场景。
- 云原生交付工作流功能公测期间无规格限制，可提交工单申请体验。
