## 작업 시나리오
Cloud Access Management(CAM)의 역할은 한 세트의 권한을 보유한 가상 신분으로, 역할 엔터티에 Tencent Cloud의 서비스, 작업 및 리소스에 대한 액세스 권한을 부여하는 데 사용합니다. 본 문서는 인스턴스 역할의 바인딩, 수정 및 삭제 등 관리 방법에 관해 소개합니다.


## 주의 사항
아래 이미지와 같이 CVM은 `cvm.qcloud.com` 등을 포함한 역할 엔터티만 바인딩하도록 지원합니다. 자세한 내용은 [역할 기본 개념](https://intl.cloud.tencent.com/document/product/598/19421)을 참조 바랍니다.
![](https://main.qcloudimg.com/raw/e47a9bc5103e3c1f342e009429e44c3a.png)


## 작업 순서

### 단일 인스턴스의 역할 바인딩/수정
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm)에 로그인한 뒤, 왼쪽 사이드바의 [인스턴스]를 선택합니다.
2. '인스턴스' 리스트 페이지에서 역할을 바인딩 또는 수정할 CVM 오른쪽의 [More]>[Instance Settings]>[역할 바인딩/수정]을 선택합니다.
3. 팝업된 '역할 바인딩/수정' 창에서 바인딩할 역할을 선택하고 [OK]를 클릭합니다.


### 여러 인스턴스의 역할 바인딩/수정
1. '인스턴스' 리스트 페이지에서 역할을 바인딩 또는 수정할 CVM을 체크하고, 상단의 [More actions]>[Instance Settings]>[역할 바인딩/수정]을 클릭합니다.
2. 팝업된 '역할 바인딩/수정' 창에서 바인딩할 역할을 선택하고 [OK]를 클릭합니다.
>?이 방식을 통하여 수정된 여러 대의 인스턴스는 역할이 모두 동일합니다.

### 단일 인스턴스의 역할 삭제
1. '인스턴스' 리스트 페이지에서 역할을 삭제할 CVM 오른쪽의 [More]>[Instance Settings]>[역할 삭제]를 선택합니다.
2. 팝업된 '역할 삭제' 창에서 [OK]를 클릭합니다.

### 여러 인스턴스의 역할 삭제
1. '인스턴스' 리스트 페이지에서 역할을 삭제할 CVM을 체크하고, 상단의 [More actions]>[Instance Settings]>[역할 삭제]를 클릭합니다.
3. 팝업된 '역할 삭제' 창에서 [OK]를 클릭합니다.
