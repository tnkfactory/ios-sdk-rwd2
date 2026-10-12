# TnkFactory iOS Reward SDK2
새롭게 출시된 보상형 SDK 입니다.

## iOS Guide

[SDK 적용 가이드](./iOS_Guide.md)

[UI 커스터마이징 가이드](./UI_Customizing.md)

[혜택플러스 연동 가이드](./PayPlus_guide.md)

[리워드플러스 연동 가이드](./RwdPlusGuide.md)

### Update Notice

* v.5.97 - 2026.10.12
  * 폴더블·iPad·가로 화면에서 광고 상세(네이티브·웹), 마이메뉴, CPS 검색, 포인트 스토어 화면이 가운데 440pt 고정 폭 대신 화면(safe area) 전체 폭을 사용. iPad 나 가로 화면을 지원하는 앱은 이 화면들이 넓어지고, 상세의 이미지·동영상 영역과 CPS 검색 결과 칸(2열 고정)도 폭에 비례해 커짐
  * 화면을 연 채로 접기/펼치기·회전·창 크기 변경으로 폭이 바뀌면 새 폭에 맞춰 다시 표시 : 네이티브 상세는 보던 위치를 유지한 채 다시 그려지며(상세 안에서 재생 중이던 동영상은 정지 상태로 돌아가고, 전체화면 재생 중에는 전체화면을 닫은 뒤에 다시 그림), 웹 상세는 페이지를 다시 불러오지 않고 폭만 바뀌며, 목록 셀·이미지 크기는 다시 계산됨
  * TnkLayout.listViewMaxWidth, TnkLayout.listViewMinWidth deprecated : 더 이상 사용하지 않음. 값을 지정하는 코드는 경고만 표시되고 그대로 빌드되지만 화면에는 영향이 없음

* v.5.96 - 2026.10.03
  * 플레이스먼트 광고 정보 필드 공개 : TnkPlacementAdItem(getAdList(), getADInfo(appId:)), TnkPlacementPubInfo(getPubInfo()) 의 필드를 앱 코드에서 직접 읽을 수 있음 (5.95 이하에서는 getAdListJson() / getPubInfoJson() 의 JSON 으로만 확인 가능)
  * AdPlacementView.onItemClick(appId:completion:) 의 completion 이 모든 경우에 한 번 호출됨 : 실패 시 TnkError 전달, TnkCode 에 에러 코드 7개 추가 (1001 ~ 1004, 1101 ~ 1103). Swift 에서 TnkCode 를 switch 할 때는 default 가 필요함
  * 폴더블·iPad·가로 화면에서 오퍼월이 앱이 지정한 폭 전체를 사용 (TnkLayout.listViewMaxWidth 는 오퍼월 목록에 적용되지 않음), 접기/펼치기·창 크기 변경 시 추천 카드·피드형 이미지 크기 재계산, 노치가 있는 iPhone 가로 화면에서는 좌우 safe area 안쪽에 표시
  * 기기 회전 관련 수정 : 카테고리 메뉴를 누른 뒤 회전하면 오퍼월 목록이 위로 밀리던 문제, 가로 화면에서 내비게이션 바 아래에 빈 띠가 생기던 문제
  * AdPlacementView.onItemClick(appId:completion:) 으로 광고에 참여할 때 이동할 URL 이 잘못되었거나 열 수 없으면 completion 이 false (TnkCode.invalidUrl) 로 전달됨 (5.95 이하에서는 true)

* v.5.95 - 2026.10.02
  * 오퍼월 테마 지정 기능 추가 : TnkStyles.offerwallTheme (.light / .dark / .system / .unspecified, iOS 에서 .system 은 .unspecified 와 같게 동작)
  * 개인정보 수집동의 해제 통보 추가 : TnkSession.setPrivacyAgreementListener(_:) / TnkPrivacyAgreementListener (리스너는 weak 로 보관되므로 매체 앱에서 강한 참조를 유지해야 함)
  * static 설치용 TnkRwdSdk2.bundle 이미지 최신화 및 Reve 레이아웃 nib 포함 (static 사용 시 TnkRwdSdk2.xcframework 와 TnkRwdSdk2.bundle 을 함께 교체해야 함)

* v.5.93 - 2026.8.28
  * 상세 페이지 직접 호출 오류 수정

* v.5.92 - 2026.8.27
  * 중복 호출 제어 추가

* v.5.90 - 2026.8.18
  * static framework 추가

* v.5.89 - 2026.8.6
  * 월 1회 참여 옵션 추가 

* v.5.82 - 2025.12.10
  * 오퍼월 리스트 아이템 비정상 정렬 수정
  * 신규 광고 아이템 유형 추가 

* v.5.77 - 2025.10.31
  * 추천 팝업 영역 디자인 커스터마이징 요소 추가

* v.5.75 - 2025.10.21
  * 추천 이벤트 영역 디자인 수정 및 커스터마이징 추가

* v.5.74 - 2025.9.24
  * 오퍼월 배너 이미지 및 포인트 radius 짤림 현상 수정

* v.5.73 - 2025.9.08
  * 사용자 간편 이벤트 팝업 인터페이스 추가

* v.5.72 - 2025.9.05
  * 광고 상세 화면 디자인 조정

* v.5.65 - 2025.8.06
  * 오퍼월 상단에 추천광고,이벤트 영역이 추가되었습니다.
  * 멀티 리워드 관련 UI 상태 표기가 추가되었으며 관련 기능이 추가되었습니다.
  * 큐레이션 관련 UI 버그가 수정되었습니다.
  * 퀴즈 관련 광고 상품 레이아웃이 추가되었습니다.
  * 쇼핑상품 즐겨찾기시 토스트 문구가 노출됩니다.
  * ios 18버전과 관련된 UI 오류 현상을 수정하였습니다.

* v.5.53 - 2025.4.22
  * 광고 리스트 생략 버그 수정
  * UI 오류 수정
  * 하단 인디케이트 관련 오류 수정

* v.5.52 - 2025.3.14
  * privacy manifest - userdefault 관련 값 변경
  * UI 오류 수정


* v.5.49 - 2025.2.18
  * 혜택 플러스 콜백 수신 버그 수정
  * UI 오류 수정
  * 캐러셀 배너 디자인 타입 추가
  * AdOfferwallViewController 카테고리 필터 랜딩 기능 추가
  
* v.5.47 - 2024.11.11
  * 혜택 플러스 콜백 수신 버그 수정

* v.5.46 - 2024.10.29
  * 기타 버그 수정

* v.5.38 - 2024.4.25
  * 쇼핑 메뉴 카테고리 필터 기능 추가
  * Privacy manifest 정리 
  * SDK 서명

* v.5.35 - 2024.2.21
  * Privacy manifest 추가
  * SDK 서명
    
* v.5.32 - 2023.12.7
  * 플레이스먼트 - PlacementFixedSizeFeedViewLayout 추가

* v.5.29 - 2023.11.3
  * 플레이스먼트 즐겨찾기 기능 오류 수정
  * 플레이스먼트 - 약관 동의 팝업 기능 수정
  * 플레이스먼트 - 광고 정보 관련 함수 추가
* v.5.28 - 2023.10.16
  * UI 커스터마이징을 위한 내부 기능 수정
  * 혜택플러스 기능 추가
* v.5.25 - 2023.09.19
  * UI 커스터마이징을 위한 내부 기능 수정
* v.5.22 - 2023.08.01
  * UI 커스터마이징을 위한 내부 기능 수정
* v.5.21 - 2023.07.19
  * UI 커스터마이징을 위한 내부 기능 수정
* v.5.20 - 2023.07.18
  * UI 커스터마이징을 위한 내부 기능 수정
* v.5.19 - 2023.07.14
  * UI 커스터마이징을 위한 내부 기능 수정
* v.5.18 - 2023.07.07
  * UI 커스터마이징을 위한 내부 기능 수정
* v.5.17 - 2023.07.05
  * 메뉴 영역에 커스텀 뷰를 추가할 수 있는 기능 추가
* v.5.16 - 2023.06.22
  * 메뉴 스크롤 방식 변경
  * CPS 검색화면에서 결제 오류 수정
  * UI 커스터마이징을 위한 내부 기능 수정
* v.5.15 - 2023.06.15
  * FontManager 기능 추가
  * darkmode 누락된 부분 추가
* v.5.14 - 2023.06.09
  * UI 커스터마이징을 위한 내부 기능 수정
* v.5.13 - 2023.06.05
  * 마이메뉴버튼 엽으로 메세지 툴팁 안띄우는 설정 추가 
* v.5.12 - 2023.06.02
  * UI 커스터마이징을 위한 내부 기능 수정
* v.5.11 - 2023.05.22
  * UI 커스터마이징을 위한 내부 기능 수정
* v.5.10 - 2023.05.15
  * TnkAlerts.showATTPopup iOS13 미만에서 오류 수정
  * OfferwallEventListener, PlacementEventListener 함수들 optional 로 변경
* v.5.09 - 2023.05.09
  * 뉴스광고 적립 방식 변경
  * 머무르기 광고 상품 기능 추가
  * 개인정보수집 동의 창 off 기능 추가 : TnkSession.sharedInstance()?.setAgreePrivacyPolicy()
  * 다크모드 색상 적용 : 다크모드 적용시 TnkColor.enableDarkMode = true
  * AdPlacementView 기능 추가 (가이드 참고) 
* v.5.06 - 2023.02.28
  * OfferwallEventListener 수정
* v.5.05 - 2023.02.27
  * 최초 출시 

