
针对每个用户，腾讯云容器服务集群在每个地域分配了固定配额。

### TKE 配额限制

每个用户可购买的 TKE 配额默认如下，如果您需要更多的配额项数量，可通过 [配额申请工单](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS) 提出配额申请。
>2019年10月21日起，用户集群支持的最大节点配额若小于5000，已调整为5000。
>


<table>
	<tr>
	<th>配额项</th>
	<th>默认值</th>
	<th>可查看入口</th>
	<th>是否可提配额</th>
	</tr>
	<tr>
	<td>单地域下集群</td>
	<td>5</td>
	<td rowspan=5><a href="https://console.cloud.tencent.com/tke2">TKE 概览页右下方</a></td>
	<td rowspan=5>是</td>
	</tr>
	<tr>
	<td>单集群下节点</td>
	<td>5000</td>
	</tr>
	<tr>
	<td>单地域下镜像命名空间</td>
	<td>10</td>
	</tr>
	<tr>
	<td>单地域下镜像</td>
	<td>500</td>
	</tr>
	<tr>
	<td>单镜像下镜像版本</td>
	<td>100</td>
	</tr>
</table>



### CVM 配额限制

腾讯云容器服务所产生的云服务器需遵守云服务器的购买限制，详情请参见[云服务器购买约束](https://intl.cloud.tencent.com/document/product/213/2664)。每个用户可购买的 CVM 配额默认如下，如果您需要更多的配额项数量，可通过 [配额申请工单](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM&level3_id=156&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%B4%AD%E4%B9%B0%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=1&scene_code=12701&step=2) 提出配额申请。

<table >
<thead>
<tr>
<th width="20%">配额项</th>
<th width="20%">默认值</th>
<th width="20%">是否可提配额</th>
</tr>
</thead>
<tbody><tr>
<td>单可用区下按量计费服务器
</td>
<td >30台或60台不等
<td>是</tr>
</thead>
</tbody></table>





### 集群配置限制
>集群配置限制集群规模， 暂不支持修改。
>

| 配置项 | 地址范围 | 影响范围 | 可查看入口 | 是否可变更 |
| ----- | ----- | ---- | --------- | ---------- |
| VPC 网络-子网 | 用户自定义设置 | 该子网可添加的节点数 |	[集群对应 VPC 子网列表页-可用 IP 数](https://console.cloud.tencent.com/vpc/subnet)	| <ul class="params"><li>不支持变更</li><li>可使用新子网</li></ul>|
| 容器网段 CIDR |	用户自定义设置 |	<ul class="params"><li>集群内节点上限</li><li>集群内 service上限</li><li>每个节点 Pod 上限</li></ul> |	集群基本信息页-容器网段 | 暂不支持变更 |

<style>
	.params{margin-bottom:0px !important;}
</style>

