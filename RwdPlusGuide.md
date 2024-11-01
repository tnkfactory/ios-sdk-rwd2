# 리워드플러스 연동 가이드 (iOS)

## 1.SDK 설정하기

해당 기능의 SDK 관련 framework 삽입 및 설정 방법은 기존의 방법과 같습니다. [SDK 적용가이드](https://github.com/tnkfactory/ios-sdk-rwd2/blob/main/iOS_Guide.md) 1.1~1.4의 안내 지침을 따라 SDK 설정후 아래 내용을 따라 설정해주시기 바랍니다.

## 2. 광고 목록 띄우기

```diff
- 주의 : 테스트 상태에서는 테스트하는 장비를 개발 장비로 등록하셔야 광고목록이 정상적으로 나타납니다.
```
링크 : [테스트 단말기 등록방법](https://github.com/tnkfactory/android-sdk-rwd/blob/master/reg_test_device.md)

다음과 같은 과정을 통해 광고 목록을 출력 하실 수 있습니다.

1) TNK SDK 초기화

2) 유저 식별값 설정

3) COPPA 설정

4) 광고 목록 출력

아래 예시 코드를 참고 하여 리워드 플러스 보상 광고 화면을 띄우실수 있습니다.

```swift
let plusInstance = LgRwdPlus.initSession(appId: "App ID") //SDK 초기화
    .setUserName("{{유저 식별 값}}") //유저 식별값 설정
    .setCOPPA(false) // COPPA 설정
plusInstance.offerwallListener = self
plusInstance.showOfferwall(self) //광고 목록 출력
```

