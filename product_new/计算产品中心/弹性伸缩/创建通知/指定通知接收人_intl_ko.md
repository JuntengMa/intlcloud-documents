사용자가 이미 공지를 작성하고 수신자를 지정한 경우, AS가 조정이 발생할 때 설정된 관련 담당자에게 알림을 발송합니다.

### 1단계: 알림 수신자 정의

[사용자 관리 콘솔](https://console.cloud.tencent.com/cam)로 이동하면 계정 등록자의 연락처 정보를 조회할 수 있습니다.

OPS 팀의 다른 팀원에 알림을 발송하는 것처럼 많은 사람들에게 알림을 발송하고 싶을 경우에는 [생성]을 클릭하여 더 많은 수신자를 생성할 수 있습니다.

>Tencent Cloud 계정을 사용자만 사용하는 경우 시스템에서 디폴트로 "개발자" 계정을 생성하므로 이 단계를 건너뛰면 됩니다.

### 2단계: 사용자 그룹 정의(수신자 분류)

AS는 **수신자**가 아니고 **사용자 그룹** 단위로 알림을 보냅니다.

**시나리오 예시:** 

- 사용자가 혼자서만 알림을 받기 원할 경우 사용자만의 연락처가 있는 사용자 그룹을 만들 수 있습니다.

- 사용자는 여러 알림 수신자를 정의했지만 알림 수신자가 같은 부서 또는 다른 부서에 있을 수 있습니다. 부서 A의 수신자에게 한 종류 알림을 보내고 부서 B의 수신자에게 다른 종류 알림을 보내기를 진행하고자 할 때 서로 다른 알림 수신자를 하나의 사용자 그룹에 포함하도록 사용자 그룹을 정의할 수 있습니다.

**설정 방법:** 
1. [사용자 그룹 관리](https://console.cloud.tencent.com/cam/groups)로 이동하여 [사용자 그룹 생성]을 클릭하고 사용자 이름을 입력한 후 [확인]을 누르십시오.
2. 그리고 [수신자 추가]를 클릭하여 해당 관련 알림 수신자를 추가하면 됩니다.

### 3단계: 사용자 그룹 사용

AS의 알람 트리거 정책 및 공지 정책을 정의할 때 알림 수신자 목록에서 정의한 사용자 그룹을 조회할 수 있으며 수요에 따라 지정된 유저 그룹으로 알림을 설정할 수 있습니다.







