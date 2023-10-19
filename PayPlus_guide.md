# 혜택플러스 연동 가이드 (iOS)

카카오 페이포인트와 연계된 보상형 오퍼월 기능이 개발되었습니다. 커스터 스키마 적용과 간단한 SDK 함수 호출을 통해 보상형 광고 화면이 노출 가능합니다.

## 1.SDK 설정하기

해당 기능의 SDK 관련 framework 삽입 및 설정 방법은 기존의 방법과 같습니다. [SDK 적용가이드](https://github.com/tnkfactory/ios-sdk-rwd2/blob/main/iOS_Guide.md) 1.1~1.4의 안내 지침을 따라 SDK 설정후 아래 내용을 따라 설정해주시기 바랍니다.

### 1.1 커스텀 스키마 xcode 등록

카카오톡 앱과의 연동을 위해 카카오 앱에서 호출할 신규 스키마를 등록해야 합니다. 해당 과정은 카카오톡과 회원정보,페이포인트와 연동하기 위한 필수 과정입니다.

Xcode > Target > Info > URL Types에 신규 Scheme를 등록합니다.

**이때 등록할 Scheme값은 타사 앱에서 등록한 스키마와 겹치지 않게 고유한 값을 기입해 주시기 바랍니다.**

아래의 이미지를 참고해 주시기 바랍니다.
![change scheme](./img/payplus_set_scheme.png)

### 1.2 혜택플러스 인스턴스 초기화

오퍼월 화면 노출은 혜택플러스 인스턴스를 통해 이루어집니다. 해당 인스턴스 사용을 위해서는 사전에 **APP-ID** 값을 발급 받으셔야합니다.  **APP-ID** 값은 [Tnk 사이트](https://tnkfactory.com) 에서 발급 받으 실 수 있습니다. **APP-ID** 값을 발급 받으셨다면 이 값을 사용하여 KaKaoTnkRwdPlus 객체가 초기화되어야합니다. 이때 [커스텀 스키마 등록](#11-커스텀-스키마-xcode-등록) 과정에서 등록한 고유 Scheme 값을 setUrlScheme 함수를 통해 함께 초기화해야 합니다.

```swift
import TnkRwdSdk2

let kakaoPlus = KaKaoTnkRwdPlus.initSession(appId: "your-app-id-from-tnk-site")
                                .setUrlScheme("{{PayPlusCustomScheme}}")
```

### 1.3 스키마 콜백 함수 연동

카카오 페이앱으로 부터 로그인이 완료된 후 데이터를 넘겨받기 위한 스키마 처리 작업을 진행해야 합니다. 넘겨 받은 스키마 url을 처리하는 코드는 아래와 같습니다.
(아래 proceedUrlDelegate 함수의 결과가 false일 경우는 혜택플러스 url이 아닌 경우입니다.)

* AppDelegate 를 사용하는 경우
  
```swift
import UIKit
import TnkRwdSdk2

@main
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?

    func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
        return KaKaoTnkRwdPlus.proceedUrlAppDelegate(open: url)
    }
}
```
* SceneDelegate 를 사용하는 경우

```swift
import TnkRwdSdk2
import UIKit

class SceneDelegate: UIResponder, UIWindowSceneDelegate {

    @available(iOS 13, *)
    func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
        _ = KaKaoTnkRwdPlus.proceedUrlSceneDelegate(openURLContexts: URLContexts)
    }
}
```  

### 1.4 오퍼월 화면 호출

위 1.3 과정까지 모두 진행하셨다면 [1.2](#12-혜택플러스-인스턴스-초기화)의 과정을 통해 만든 인스턴스의 showOfferWall함수를 호출하시면 광고 화면을 노출할 수 있습니다.

```swift
import TnkRwdSdk2

let kakaoPlus = KaKaoTnkRwdPlus.initSession(appId: "your-app-id-from-tnk-site")
                                .setUrlScheme("{{PayPlusCustomScheme}}")
kakaoPlus.showOfferwall(self)

```
