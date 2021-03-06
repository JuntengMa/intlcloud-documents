### 과금 개요

과금형 예약 인스턴스(Reserved Instance Offering)는 계정 내 종량제 인스턴스를 응용한 일종의 차감식 과금 방식으로, 예약 인스턴스가 정상적인 라이프사이클에 있고, 예약 인스턴스와 속성이 완벽히 일치해야만 종량제 청구서에서 요금이 차감되도록 적용할 수 있습니다. 예약 인스턴스는 종량제 과금 모드와 비교해 가격이 더 합리적입니다.
>? 예약 인스턴스는 현재 베타 서비스 중입니다. 가격 문서는 참조용이며 최종 가격은 청구서를 기준으로 적용됩니다. 사용을 원하시면 [영업팀에 문의](https://intl.cloud.tencent.com/contact-sales) 바랍니다.
>

> 과금형 예약 인스턴스는 현재 환불할 수 없습니다.
>
> 과금형 예약 인스턴스는 설정을 변경할 수 없습니다. 과금형 예약 인스턴스와 매칭된 종량제 인스턴스의 설정을 변경하면 과금형 예약 인스턴스의 요금 혜택을 누릴 수 없습니다.
>
> 과금형 예약 인스턴스와 매칭된 종량제 인스턴스를 셧다운(Shutdown) 하거나 강제 셧다운 해도 종량제 인스턴스에서 과금형 예약 인스턴스의 요금 차감 서비스를 계속 이용할 수 있습니다.


#### 출시 일정

과금형 예약 인스턴스 기능은 현재 화이트리스트 형식으로 제공되고 있습니다. 과금형 예약 인스턴스 [베타 신청](https://intl.cloud.tencent.com/apply/p/bvrqmrrp5ns)에서 사용 자격을 신청하시기 바랍니다. 

#### 속성

- [리전](https://cloud.tencent.com/document/product/213/6091): 리전은 물리적 데이터센터의 지리적 위치입니다. 예: 실리콘밸리
- [가용존](https://cloud.tencent.com/document/product/213/6091): 가용존(Zone)은 같은 리전 안에서 전력과 네트워크가 서로 독립된 Tencent Cloud의 물리적 데이터센터입니다. 예: 실리콘밸리 1존
- [인스턴스 유형](https://cloud.tencent.com/document/product/213/11518): Tencent Cloud에서는 다양한 인스턴스 유형을 제공합니다. 예: 표준형
- [인스턴스 사양](https://cloud.tencent.com/document/product/213/11518): 과금형 예약 인스턴스의 모델 사양입니다. 예: S4.SMALL1 
- 운영 체제: Linux

> 과금형 예약 인스턴스가 정상적인 라이프사이클에 있고, 예약 인스턴스와 속성이 완벽히 일치해야만 종량제 청구서에서 요금이 차감되도록 적용할 수 있습니다.

#### 개념 비교

| 비교 항목   | 과금형 예약 인스턴스      | 종량제 인스턴스         |
| -------- | ---------- | ---------- |
| 형태     | 과금 모드의 일종, 사용량 과금 인스턴스의 요금을 차감하는 방식.       | [종량제](https://intl.cloud.tencent.com/document/product/213/2179) 방식으로 구매한 인스턴스, 실제로 실행되는 가상 컴퓨터와 같다. |
| 사용 방법 | 개별 사용 불가. 종량제 인스턴스와 매칭하여 사용할 수 있으며, 종량제 인스턴스 청구서에서 차감. | 개별 관리 및 설정할 수 있고 심플형 웹 서버로써 이용할 수 있으며, 다른 Tencent Cloud 제품과 조합하여 고효율적인 솔루션 제공. |

#### 사용 제한

현재 과금형 예약 인스턴스로 구매할 수 있는 가용존 및 인스턴스 사양은 API[구매 가능한 과금형 예약 인스턴스 목록](https://intl.cloud.tencent.com/document/product/213/30575)에서 조회하시기 바랍니다.

운영 체제: 현재 Tencent Cloud의 과금형 예약 인스턴스는 Linux 운영 체제만 지원합니다

결제 방식: 전체 선불, 일부 선불, 선불금 없음 이 세 가지 방식을 제공합니다

유효기한: 1년

쿼터: 한 사용자는 각 가용존에서 매달 최대 20대의 과금형 예약 인스턴스를 보유할 수 있습니다
