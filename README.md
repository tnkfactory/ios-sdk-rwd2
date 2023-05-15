# TnkFactory iOS Reward SDK2
새롭게 출시된 보상형 SDK 입니다.

## iOS Guide

[SDK 적용 가이드](./iOS_Guide.md)

[UI 커스터마이징 가이드](./UI_Customizing.md)

### Update Notice

* v.6.10 - 2023.05.15
  * TnkAlerts.showATTPopup() iOS13 미만에서 오류 수정
  * OfferwallEventListener, PlacementEventListener 함수들 optional 로 변경
* v.6.09 - 2023.05.09
  * 뉴스광고 적립 방식 변경
  * 머무르기 광고 상품 기능 추가
  * 개인정보수집 동의 창 off 기능 추가 : TnkSession.sharedInstance()?.setAgreePrivacyPolicy()
  * 다크모드 색상 적용 : 다크모드 적용시 TnkColor.enableDarkMode = true
  * AdPlacementView 기능 추가 (가이드 참고) 
* v.5.06 - 2023.02.28
  * OfferwallListener 수정
* v.5.05 - 2023.02.27
  * 최초 출시 

