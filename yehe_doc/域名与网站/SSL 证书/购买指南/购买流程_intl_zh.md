证书购买前，建议您先了解各证书种类以及域名类型的区别，进而根据您实际需求选择合适的证书。以下将为您介绍购买证书的流程：

### 步骤1：登录 SSL 证书购买页
1. 登录 [SSL 证书购买页](https://console.cloud.tencent.com/ssl)。
2. 详细参考官网售卖提供的参数对比。如下图所示：
![](https://main.qcloudimg.com/raw/6e6fe4d37a533f2b81f1f70abf76ef8f.png)


### 步骤2：选择证书种类及证书品牌
1. 请根据您的行业以及实际需求选择相应的证书种类。具体请参考 [各证书类型案例](https://intl.cloud.tencent.com/document/product/1007/37811)。
2. 关于证书品牌的介绍请参考 [证书品牌介绍](https://intl.cloud.tencent.com/document/product/1007/37810)。

### 步骤3：选择域名类型及支持的域名数目
<table>
<tr>
<th>域名类型</th>
<th>描述</th>
<th>注意事项</th>
</tr>
<tr>
<td>单域名</td>
<td>只支持绑定1个域名，可以支持绑定二级域名 tencent.com、或是三级域名 example.tencent.com。</td>
<td><li>不支持绑定二级域名下的所有子域名。</li><li>域名级数最多可以支持100级。</li><li>绑定 www.tencent.com 域名（子域名是 www）的 SSL 证书，会同时支持 tencent.com 二级域名。</li></td>
</tr>
<tr>
<td>多域名</td>
<td>单个证书可以绑定多个域名，最多可以支持数量以控制台展示为准。</td>
<td><li>SecureSite 多域名证书的价格即按域名数目进行叠加。</li><li>GeoTrust、TrustAsia、GlobalSign、Wotrus、DNSPod 多域名证书除默认支持域名数量外，附加域名再另叠加计价。</li></td>
</tr>
<tr>
<td>泛域名</td>
<td>支持绑定一个且只有一个泛域名，泛域名只允许添加一个通配符。</td>
<td><li>例如，\*.tencent.com，\*.example.tencent.com，最多支持100级。</li><li>例如，\*.\*.tencent.com 多个通配符的泛域名是不支持的。</li><li>绑定 \*.tencent.com 域名（必须是二级泛域名）的 SSL 证书，会同时支持 tencent.com 二级域名。</li></td>
</tr>
<tr>
<td>通配符多域名</td>
<td>支持绑定多个泛域名。</td>
<td>例如，\*.tencent.com、\*.ssl.tencent.com、\*.another.com，共计3个泛域名，包含同一级的全部子域名，最多可以支持数量以控制台展示为准。</td>
</tr>
</table>

### 步骤4：选择证书年限
由于苹果和谷歌根存储政策的变化，自2020年9月1日起，政策禁止使用有效期超过13个月（397天）新颁发的 SSL/TLS 证书。因此，自2020年9月1日起，全球 CA 认证机构不再签发2年期 SSL 证书，**默认只能购买1年期 SSL 证书**。详情请查看：[关于 CA 机构于2020年9月1日起停止签发为期两年 SSL 证书的通知](https://intl.cloud.tencent.com/document/product/1007/38090)。

### 步骤5：订单支付
完成品牌、型号、支持域名、和证书年限的选择后，则可以提交订单，继续完成支付流程。


### 步骤6：提交证书申请
- **DNSPod 品牌证书 OV 与 EV 型 SSL 证书：**
购买证书完成后，需在 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl) 中提交审核材料进行证书申请和域名所有权认证，提交申请后，需人工审核。待人工审核及域名认证均通过后，才可颁布证书。
- **Wotrus 品牌证书 OV 与 EV 型 SSL 证书：**
购买证书完成后，需在 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl) 提交材料进行证书申请和域名所有权认证，提交申请后，需人工审核。审核通过后即可进行域名所有权验证，CA 机构审核通过后将签发证书。
- **其他品牌 OV 与 EV 型 SSL 证书：**
购买证书完成后，需在 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl) 中提交审核材料进行证书申请，CA 机构审核通过后将签发证书。详情请查看 [其他品牌 OV 与 EV 型证书材料提交流程](https://intl.cloud.tencent.com/document/product/1007/30160)。
- **域名型（DV）SSL 证书：**
购买证书完成后，需在 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl) 提交材料进行证书申请和域名所有权认证，提交申请后，即可进行域名所有权验证，CA 机构审核通过后将签发证书。
- **域名型（DV）免费 SSL 证书：**
购买证书完成后，需进行域名所有权认证，CA 机构审核通过后将签发证书。

