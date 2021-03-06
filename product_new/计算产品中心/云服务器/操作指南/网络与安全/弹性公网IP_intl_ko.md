## 작업 시나리오
EIP 주소 또는 EIP입니다. 클라우드 컴퓨팅 동적 설계를 위한 정적 IP 주소로써, 어느 리전 아래 하나의 변하지 않는 고정 공용 네트워크 IP 주소입니다. EIP 주소의 도움으로 주소를 계정 중의 다른 인스턴스 또는 [NAT Gateway 인스턴스](/doc/product/215/%E7%BD%91%E5%85%B3#2.-nat.E7.BD.91.E5.85.B3)로 다시 매핑하거나, 인스턴스 장애를 차단할 수 있습니다. 본 문서는 EIP 주소의 사용 방법에 대해 소개합니다.

## 전제 조건

[CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인되어 있어야 합니다.

## 작업 순서

### EIP 신청 

1. 왼쪽 사이드바에서 [[EIP](https://console.cloud.tencent.com/cvm/eip)]를 클릭해 EIP 관리 페이지로 진입하십시오.
2. EIP 관리 페이지에서 [신청]을 클릭하십시오.
3. 팝업된 “EIP 신청” 창에서 리전 선택, IP 주소 유형 설정, 과금 방식 및 대역폭 최댓값, 수량을 입력하십시오.
4. [확인]을 클릭한 뒤 EIP 신청을 완료하십시오.
신청이 끝나면 리스트에서 사용자가 신청한 EIP를 확인할 수 있으며, 이때는 바인딩이 되지 않은 상태입니다.

<span id = "jump2">  </span>
### 클라우드 제품의 EIP 바인딩

1. 왼쪽 사이드바에서 [[EIP](https://console.cloud.tencent.com/cvm/eip)]를 클릭해 EIP 관리 페이지로 진입하십시오.
2. EIP 관리 페이지에서 바인딩할 클라우드 제품의 EIP를 선택한 뒤 [더 보기]>[바인딩]을 클릭하십시오.
> 바인딩 시 EIP가 이미 인스턴스에 바인딩되어 있는 경우에는 바인딩을 먼저 해제하십시오.
>
3. 팝업된 “리소스 바인딩” 창에서 바인딩할 EIP의 리소스를 선택하고 [확인]을 클릭하십시오.
4. 팝업된 “EIP 바인딩” 표시 상자에서 [확인]을 클릭하면 클라우드 제품의 바인딩이 완료됩니다.


### 클라우드 제품의 EIP 바인딩 해제

1. 왼쪽 사이드바에서 [[EIP](https://console.cloud.tencent.com/cvm/eip)]를 클릭해 EIP 관리 페이지로 진입하십시오.
2. EIP 관리 페이지에서 바인딩 해제할 클라우드 제품의 EIP를 선택하고 [더 보기]>[바인딩 해제]를 클릭하십시오.
3. 팝업된 “EIP 바인딩 해제” 창에서 바인딩 해제 정보를 확인하고 [확인]을 클릭하십시오.
4. 팝업된 “EIP 바인딩 해제” 표시 상자에서 [확인]을 클릭하면 즉시 클라우드 제품의 바인딩 해제가 완료됩니다.
> 바인딩 해제 후 클라우드 제품의 인스턴스는 새로운 공용 네트워크 IP를 할당받게 되며, 새로 할당받은 공용 네트워크 IP는 바인딩 전의 공용 네트워크 IP와 불일치할 수 있습니다.
>

<span id = "jump">  </span>
### EIP 릴리스

1. 왼쪽 사이드바에서 [[EIP](https://console.cloud.tencent.com/cvm/eip)]를 클릭해 EIP 관리 페이지로 진입하십시오.
2. EIP 관리 페이지에서 릴리스할 클라우드 제품의 EIP를 선택하고 [더 보기]>[릴리스]를 클릭하십시오.
3. 팝업된 “EIP 릴리스” 창에서 릴리스할 EIP를 입력하고 [확인]을 클릭하십시오.
4. 팝업된 “EIP 릴리스” 표시 상자에서 [확인]을 클릭하면 릴리스가 완료됩니다.

### 대역폭 조정
1. 왼쪽 사이드바에서 [[EIP](https://console.cloud.tencent.com/cvm/eip)]를 클릭해 EIP 관리 페이지로 진입하십시오.
2. EIP 관리 페이지에서 대역폭 조정이 필요한 EIP를 선택하고 [대역폭 조정]을 클릭하십시오.
3. 팝업된 “대역폭 조정” 창에서 목표 대역폭 값을 설정하고 [확인]을 클릭하면 대역폭 조정이 완료됩니다.

### 공용 네트워크 IP를 EIP로 전환
구매한 CVM(Cloud Virtual Machine) 인스턴스에 따라 함께 구매한 공용 네트워크 IP가 일반 공용 네트워크 IP일 경우, 탄력적 기능이 없어 마운트와 언마운트가 불가능합니다. 아래의 작업 절차를 따라서 일반 공용 네트워크 IP를 EIP로 전환하십시오.
1. 왼쪽 사이드바에서 [[인스턴스](https://console.cloud.tencent.com/cvm/index)]를 클릭해 인스턴스 관리 페이지로 진입하십시오.
2. EIP로 전환할 인스턴스를 선택하고 <img src="https://main.qcloudimg.com/raw/25e8c0e37b73c12da900301f03e57dbc.png" style="margin: 0;"></img>클릭하십시오. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/53b608b2bb0840920703e7f50957611a.jpg)
3. 팝업된 “EIP로 전환” 창에서 [전환 확인]을 클릭하십시오.
![](https://main.qcloudimg.com/raw/3d20c058c66975f847e68e42ae944d6f.png)

## 비정상 상태 조사
일반적으로 아래와 같은 원인으로 EIP 주소가 네트워크와 통하지 않는 비정상 상황이 나타날 수 있습니다. 
- EIP 주소가 클라우드 제품에 바인딩되어 있지 않습니다. 구체적인 바인딩 방법은 [클라우드 제품의 EIP 바인딩](#jump2)을 참조하십시오.
- 보안 정책이 무효 상태입니다. 보안 정책(보안 그룹 또는 네트워크 ACL)이 유효한지 조회하십시오. 만약 바인딩된 클라우드 제품 인스턴스에 8080 포트 액세스 금지와 같은 보안 정책이 있을 경우에도 EIP의 8080 포트에 액세스할 수 없습니다.
