오토 스케일링(Auto Scaling, AS)은 서비스 부하에 따라 자동으로 용량 확장 및 축소를 지원하는 것 외에도 수동 조작을 지원하여 빠른 수동 용량 확장 및 축소하는 효과를 달성합니다. 다음 두 가지 방법으로 용량 확장 효과를 달성할 수 있습니다.
- [스케일링 그룹에 기존 CVM 용례 추가](# func1)
- [스케일링 그룹의 원하는 용량을 수정하여 원 클릭 용량 확장을 실행](# func2)


<span id = "func1"></span>
## 스케일링 그룹에 기존 CVM 용례를 추가합니다.
스케일링 그룹에 기존 용례를 추가하는 방식을 제공하여 스케일링 그룹의 다른 기기와 함께 부하를 모니터링하고 관리할 수 있는 기능을 구현합니다.

### 전제 조건
- 용례가 실행 중인 상태입니다.
- 용례와 스케일링 그룹은 같은 리전에 있습니다.
- 용례의 네트워크 속성은 스케일링 그룹과 동일해야 합니다. 즉, 동일한 기본 네트워크에 속하거나 동일한 사설 네트워크에 속해야 합니다.

### 설명 사항
- AS는 해당 그룹의 필요한 용량과 추가할 용례 수를 서로 더합니다.
  예를 들어, 스케일링 그룹의 현재 원하는 용량은 5이고 수동으로 3대의 용례를 추가하면 스케일링 그룹의 원하는 용량은 5+3=8로 변경됩니다. 추가할 용례 수에 필요한 용량을 더한 값이 스케일링 그룹의 최대 용례 수를 초과할 경우, 요청이 거절됩니다.
- 스케일링 그룹은 1개 또는 여러 Cloud Load Balancer(CLB)와 연결되며 수동으로 추가된 용례는 스케일링 그룹의 모든 CLB에 자동으로 등록됩니다.
- 스케일링 그룹이 용량 축소될 경우, 자동으로 생성된 기기를 먼저 제거하고, 자동으로 생성된 기기가 없을 경우, 수동으로 추가된 기기가 제거됩니다.
- 스케일링 그룹이 수동으로 추가된 용례를 삭제할 경우, 용례를 스케일링 그룹과 CLB에서 삭제하면 더 이상 스케일링 그룹을 통해 관리되지 않고 종료되지 않습니다.

### 콘솔을 사용하여 수동으로 용례 추가
1. [스케일링 그룹 콘솔](https://console.cloud.tencent.com/autoscaling/group)에 로그인하고 추가할 용례의 스케일링 그룹 ID를 추가하십시오.
2. 다음과 같이 스케일링 그룹 세부 정보 페이지로 이동하여 [용례 연결]> [용례 추가]를 선택하십시오.
![](https://main.qcloudimg.com/raw/0b4442a883c8cbd318608b0a955174c7.png)
3. 다음과 같이 대화 상자에서 해당하는 용례를 선택하고 [확인]을 클릭하십시오.
![](https://main.qcloudimg.com/raw/149a4bd4a05c27754820de3a988eb7c4.png)

<span id = "func2"></span>
## 원하는 용량으로 수정하여 원 클릭 용량 확장을 실행합니다.
### 용량 확장 시나리오
요구 사항이 다음과 같은 시나리오에 부합되면 [콘솔에서 원 클릭 용량 확장을 실행] (# step1)합니다. 사전에 CLB 전달 규칙, 기기 구성 및 서비스 배치를 먼저 수행하고, 후속 서비스의 용량을 확장해야 할 경우에도 원 클릭으로 스케일링 그룹의 파라미터를 수정하여 신속하게 용량 확장을 완료합니다.
- 서비스의 최고점과 파동을 예측이 어렵기 때문에 용량 확장 및 축소를 완전히 시스템에 맡기는 것을 권장하지 않습니다. 그러나, 서비스의 최고점과 파동을 예측 가능하며 자세한 내용은 [온타임 퀘스트 관리](https://intl.cloud.tencent.com/document/product/377/3591)를 참조하십시오.
- 컴퓨팅 요구 사항은 예를 들어 여론 조사, DNA 시퀀싱, 기상 관측 등과 같이 프로젝트 지향적이며 매번 사용되는 기기와 유사합니다.


<span id = "step1"></span>
### 콘솔에서 원 클릭으로 용량 확장 실행
다음 절차를 실행하여 CVM 템플릿을 시작 구성으로 설정하고 해당하는 스케일링 그룹을 구성합니다.

1. 사용자 지정 이미지를 생성하려면 [사용자 지정 이미지를 생성하는 자세한 방법](https://intl.cloud.tencent.com/document/product/213/4942)을 참조하십시오.
 >
 >- 후속으로 용량 확장된 용례는 해당 이미지에 따라 환경을 배포합니다.
 >- 사용자 지정 이미지 생성을 위한 TIP: 1개의 기존 CVM을 선택하거나 새로운 CVM을 생성하여 서비스를 배치하고, 서비스를 시스템 퀘스트와 함께 시작하도록 설정한 다음 사용자 지정 이미지로 내보낼 수 있습니다.
2. 해당 사용자 지정 이미지에 따라 시작 구성을 생성합니다. 자세한 내용은 [시작 구성 만들기](https://intl.cloud.tencent.com/document/product/377/8544)를 참조하십시오.
3. [스케일링 그룹 만들기](https://intl.cloud.tencent.com/document/product/377/8551)
생성 시 시작 구성을 선택하고 최소 스케일링 수, 최대 스케일링 수, 최초 용례 수를 필요로 하는 서버의 최솟값, 최댓값 및 현재 수량에 따라 입력합니다.
4. 위의 절차를 완료한 후 서비스 용량 확장이 필요할 경우(예: DNA 시퀀싱 퀘스트을 시작 또는 청구 시스템을 통한 데이터 수집) 스케일링 그룹 구성을 수정하여 최소 스케일링 수, 최대 스케일링 수 및 원하는 용량을 업그레이드 시킴으로써 AS는 신속하게 용량 확장을 완료할 수 있습니다.






