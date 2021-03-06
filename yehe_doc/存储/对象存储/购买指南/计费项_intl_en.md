Billable items in COS include [storage usage](#jf1), [requests(#jf2), [data retrievals](#jf3), [traffic](#jf4), and [administrative features](#jf5). The following describes each billable item in detail. After learning about them and the [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239), you will be able to estimate fees on your own.


> ?COS offers 3 object storage classes for different access frequencies: STANDARD, STANDARD_IA, and ARCHIVE. For more information, see [Storage Classes](https://intl.cloud.tencent.com/document/product/436/30925).


<span id="jf1"></span>

## Storage Usage Fees

| Billable Item   | Applicable Storage Class&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                               | Definition                                                   | Billing Description                                                     |
| -------- | -------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Storage usage |STANDARD<br>STANDARD_IA<br>ARCHIVE| Storage usage is the actual storage space consumed by your data. It is billed based on the size of the storage capacity you actually use.  |<li>Monthly billing cycle<br><li>Storage usage fees = storage usage unit price * monthly storage usage<br><li>Monthly storage usage = sum of "daily storage usage" in the month / number of days in the month<br><li>Daily storage usage = sum of "5-minute storage usage" / 288 (number of statistical points) |



#### Billing restrictions

1. STANDARD_IA storage class: if the storage duration is less than 30 days, it will be calculated as 30 days. If a single stored file is less than 64 KB, it will be calculated as 64 KB; otherwise, files are calculated based on their actual size.
2. ARCHIVE storage class: this storage class is available in Public Cloud regions only. If the storage duration is less than 90 days, it will be calculated as 90 days. If a single stored file is less than 64 KB, it will be calculated as 64 KB; otherwise, files are calculated based on their actual size.
3. If you upload an object successfully to STANDARD_IA or ARCHIVE storage class with versioning not enabled, COS will delete any existing objects of the **same name**. In this case, storage fees will still be incurred for **the deleted objects** for a minimal storage duration.

<span id="jf2"></span>

## Request Fees

Request fees include the fees incurred by **user requests** and **backend requests** generated by feature configuration.

- User requests: you can perform upload, download, query, delete and other operations via APIs, SDKs or the console by sending requests to Tencent COS.
- Backend requests: these include requests to transition objects, delete expired STANDARD copies restored from ARCHIVE, read/write data for cross-region replication, and deliver inventory reports.

| Billable Item   | Applicable Storage Class&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                               | Definition                                                   | Billing Description                                                     |
| -------- | -------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Number of requests | STANDARD<br>STANDARD_IA<br>ARCHIVE | Calculated based on the number of requests sent|  <li>Monthly billing cycle<br><li>If the accumulated number of requests is below 10,000, it will be calculated as 10,000 requests<br><li>Request fees = unit price per 10,000 requests * monthly accumulated number of requests / 10,000 (rounded down) |

#### Billing restrictions

1. Both successful and failed requests are billable.
2. 10,000 requests serve as the smallest counting unit for request fees; therefore, if the number of monthly accumulated requests is below 10,000 it will be calculated as 10,000 requests, no matter whether a request succeeds or fails.
3. When archived data is read, the data is first restored to the STANDARD storage class and then read there; therefore, the number of requests is counted in the STANDARD storage class.

<span id="jf3"></span>

## Data Retrieval Fees



| Billable Item | Applicable Storage Class | Definition | Billing Description |
| ---------- | ---------------------- | -------------------------------- | ------------------------------------------------------------ |
| Data retrieved | STANDARD_IA<br />ARCHIVE | Calculated based on the amount of data retrieved | <li>Monthly billing cycle<br /><li>Data retrieval fees = unit price per GB * monthly amount of data retrieved |

#### Billing restrictions

**STANDARD_IA** and **ARCHIVE** are designed to store cold data. To download object data from these two storage classes, you need to retrieve it first, thereby incurring both retrieval fees and download traffic fees.

<span id="jf4"></span>

## Traffic Fees

Traffic fees are calculated based on the accumulated traffic generated by storage data reads.

<table>
   <tr>
      <th>Billable Item</th>
      <th>Applicable Storage Class</th>
      <th>Definition</th>
      <th>Billing Description</th>
   </tr>
   <tr>
      <td>Public network upstream traffic</td>
      <td rowspan="7" nowrap="nowrap">STANDARD<br>STANDARD_IA<br>ARCHIVE</td>
      <td>Traffic generated by data transfer from the client to COS over the Internet</td>
      <td>Free</td>
   </tr>
   <tr>
      <td>Private network upstream traffic</td>
      <td>Traffic generated by data transfer from the client to COS over Tencent Cloud private network</td>
      <td>Free</td>
   </tr>
   <tr>
      <td>Public network downstream traffic</td>
      <td>Traffic generated by data transfer from COS to the client over the Internet</td>
      <td><li>Daily billing cycle<br><li>Public network downstream traffic fees = unit price per GB * daily accumulated public network downstream traffic</td>
   </tr>
   <tr>
      <td>Private network downstream traffic</td>
      <td>Traffic generated by data transfer from COS to the client over the Tencent Cloud private network</td>
      <td>Free</td>
   </tr>
   <tr>
      <td>CDN origin-pull traffic</td>
      <td>Traffic generated by data transfer from COS to a Tencent Cloud CDN edge server</td>
      <td><li>Daily billing cycle<br><li>Public network downstream traffic fees = unit price per GB * daily accumulated public network downstream traffic</td>
   </tr>
   <tr>
      <td>Cross-region replication traffic</td>
      <td>Traffic generated by replicating data from a bucket in one region to a bucket in another region</td>
      <td><li>Daily billing cycle<br><li>Cross-region replication traffic fees = unit price per GB * daily accumulated cross-region replication traffic</td>
   </tr>
   <tr>
      <td>Global acceleration traffic</td>
      <td>Traffic generated by data transfer using an acceleration endpoint through the global acceleration feature. This traffic consists of upstream traffic and downstream traffic:<br><li>Upstream traffic is the traffic generated by data upload to COS using an acceleration endpoint<br><li>Downstream traffic is the traffic generated when viewing or downloading COS data using an acceleration endpoint</td>
      <td><li>Daily billing cycle<br><li>Global acceleration traffic fees = unit price per GB * daily accumulated global acceleration traffic</td>
   </tr> 
</table>

#### Billing restrictions

1. When archived data is read, the data is first restored to the STANDARD storage class and then read there; therefore, the traffic is counted in the STANDARD storage class.
2. CDN origin-pull traffic refers to the traffic generated by data transfer from COS to a Tencent Cloud CDN edge server. If traffic is forwarded from a third-party origin server to COS, public network downstream traffic will be generated.

> ?
>
> - Tencent Cloud products within the same region access each other over the private network by default and no traffic fees will be incurred. For more information on how to identify private network access, please see [COS Access via Private Network and Public Network](https://intl.cloud.tencent.com/document/product/436/30613?lang=en&pg=#cos-access-via-private-network-and-public-network).
> - Public network downstream traffic consists of the traffic generated by downloading objects through **object URLs** and browsing objects through **static website access nodes**.
> - CDN origin-pull traffic refers to traffic generated by browsing or downloading COS data from the client through **CDN acceleration endpoints** after CDN acceleration is enabled.
> - Cross-region replication traffic is generated when you replicate data from a bucket in one region to a bucket in another region using APIs or the cross-region replication feature.

#### Traffic trends

The figure below shows the traffic fees incurred by data transmitted from COS to an end user with CDN acceleration enabled and disabled, respectively.
![](https://main.qcloudimg.com/raw/a7e5562e9404ba265cb4797a59521d28.png)

<span id="jf5"></span>

## Administrative Feature Fees

Administrative feature fees are calculated based on the use of enabled administrative features, such as inventory and COS select.



<table>
<thead>
<tr>
<th>Billable Item</th>
<th>Applicable Storage Class</th>
<th>Definition</th>
<th>Billing Description</th>
</tr>
</thead>
<tbody><tr>
<td>Inventory feature fees</td>
<td nowrap="nowrap">STANDARD<br>STANDARD_IA<br>ARCHIVE</td>
<td>Fees incurred from listing bucket objects after the inventory feature is enabled</td>
<td><li>Daily billing cycle<br></li><li>Billed per million objects listed</li></td>
</tr>
<tr>
<td>COS select fees</td>
<td>STANDARD storage</td>
<td>Fees incurred from extracting objects when the COS select feature is enabled</td>
<td><li>Daily billing cycle<br></li><li>Billed by the size of data extracted</li></td>
</tr>
<tr>
<td>Batch operation fees</td>
<td nowrap="nowrap">STANDARD<br>STANDARD_IA<br>ARCHIVE</td>
<td>Once you enable the batch operation feature, COS will bill you based on the number of jobs created and object operations</td>
<td><li>Daily billing cycle<br></li><li>Billed by the number of jobs created and object operations</li></td>
</tr>
<tr>
<td>Object tagging fees</td>
<td nowrap="nowrap">STANDARD<br>STANDARD_IA<br>ARCHIVE</td>
<td>Once you enable the object tagging feature, COS will bill you based on the number of object tags</td>
<td><li>Daily billing cycle<br></li><li>Billed by the number of object tags you set</li></td>
</tr>
</tbody></table>

