**In order to use the Tencent Cloud Key Management Service (the "KMS" or the "Service"), you should read and observe this Key Management Service Level Agreement (this "Agreement", or this "SLA") and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, *among others*, the terms and definitions of the Service, Service availability and Service uptime metrics, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, may be in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking "Agree"/ "Next", or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

## 1. Terms and Definitions

1.1  **Key Management Service (KMS)**: means a key service protecting the security of data and keys, by which a higher level of security of your information (including data and keys) will be ensured. For details, please refer to the Service you purchase, and the contents of the Service provided by Tencent Cloud.

1.2 **Failed Request**: means a request with a returned error code "InternalError", excluding those in any circumstance as provided for in the release of liabilities provisions below.

1.3 **Valid Request**: means a request received by KMS server, excluding those in any circumstance as provided for in the release of liabilities provisions below.

1.4  **Error Rate Per Five Minutes**: Error Rate Per Five Minutes = the number of Failed Requests per five minutes / the total number of Valid Requests per five minutes × 100%

1.5  **Service Month(s)**: means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The availability of the Service will be calculated independently for each Service Month.

1.6 **Monthly Service Fee**: means KMS Service fees under your Tencent Cloud account within a Service Month.

## 2. Service Availability

**2.1 Calculation of Service Uptime Rate**

Service Availability = 1 -- (the sum of the Error Rate Per Five Minutes within a Service Month / the total number of five-minute measurement units within a Service Month) × 100%

**2.2 Standard of Service Metrics**

**The Service Availability of the Service will be** **no less than 99.90%**. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned guaranteed standard, other than in any circumstance as provided for in the release of liabilities provisions below.

## 3. Service Compensation

In respect of this Service, if the Service Availability is less than 99.90%, you will be entitled to compensations in accordance with the following terms:

**3.1 Standards of Compensation**

(1) Compensations will be made **in the form of voucher** by Tencent Cloud, and you should follow the rules for using the voucher (including the valid term; for details, please refer to the rules of vouchers published on Tencent Cloud's official website). You cannot redeem such voucher for cash or request to issue an invoice for such voucher. Such voucher can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability for a Service Month fails to meet the standard, the amount of compensation will be calculated for such month independently, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by the user for such month** (the Monthly Service Fee referred to herein shall exclude the portion deducted by a voucher or promotional credit or any other non-cash portion).

|**Service Availability (Av) for a Service Month**|   **Value of Compensation Voucher**|
|--------------------------------------------| -----------------------------------|
|99.90% > Av ≥ 99%	|10% of the Monthly Service Fee|
|99% > Av ≥ 95%	|25% of the Monthly Service Fee|
|95% > Av|	100% of the Monthly Service Fee|


**3.2 Time Limit for Compensation Application**

(1) If the Service Availability for a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the fifth (5^th^) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail**.

(2) **You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard**. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

## 4. Release of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service downtime shall not be counted towards Service unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**
4.1	any scheduled downtime due to any system maintenance with prior notice by Tencent Cloud, including system cutover, upgrade and malfunction simulation test.
4.2	any malfunction or configuration adjustment of any network or equipment that is not Tencent Cloud facility.
4.3	any Service unavailability attributable to any person other than Tencent Cloud, such as hacker attack or negligence of your third-party supplier.
4.4	any loss or leak of data, passcode or password due to your improper maintenance or improper confidentiality measures.
4.5	any mal-operation due to your negligence, or any operation authorized by you.
4.6	any failure of a user to abide by user guide or suggestions for using Tencent Cloud products, including without limitation:
  (1)	loss of the key to an account password and envelope encryption, resulting in the decryption failure of underlying data.
  (2)	failure to clear cache in a timely manner for envelope encryption, resulting in the leak of the plaintext of the key.
  (3)	deletion of CMK by mal-operation, resulting in the decryption failure of underlying data.
  (4)	other incorrect operation, resulting in the leak of data or decryption failure.
4.7	any request made by a user who has not yet activated the Service or has any unpaid overdue payment.
4.8	any event of force majeure.
4.9	any Service unavailability or failure of the Service to meet the availability standard due to any reason not attributable to Tencent Cloud.
4.10	any other circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately.


## 5. Miscellaneous

5.1	The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.
5.2	Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.
5.3	As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)

