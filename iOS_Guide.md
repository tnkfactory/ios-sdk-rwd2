## 1. SDK 설정하기

### 라이브러리 다운로드

### 라이브러리 등록
다운로드 받은 SDK 압축파일을 풀면 TnkRwdSdk2.xcframework 폴더가 생성됩니다. 해당 폴더를 적용하고자 하는 XCode 프로젝트 폴더로 이동시키세요.

폴더를 이동시켰으면 ...

아래의 이미지를 참고하세요.

### 앱추적동의

앱 광고의 경우 유저들의 광고 참여여부를 확인하기 위해서는 사전에 앱추적동의를 받아야합니다.  앱추적동의는 iOS 14부터 제공되는 기능으로 기기의 IDFA 값 수집을 위하여 필요합니다. 앱 추적동의 창은 가급적이면 개발하시는 앱이 시작되는 시점에 띄우는 것을 권고드립니다.  [앱 추적동의에 대하여 더 알아보기](https://developer.apple.com/kr/app-store/user-privacy-and-data-use/)

#### 앱 추적동의창 띄우기

앱 추적동의 창을 띄우기 위해서는 우선 info.plist 파일에 아래와 같이 "Privacy - Tracking Usage Description" 문구를 추가합니다.  추가한 문고는 앱 추적 동의 팝업 창에 노출됩니다.

작성 예시) 사용자에게 최적의 광고를 제공하기 위하여 광고활동 정보를 수집합니다.
 
<이미지>

아래의 API 를 호출하여 앱 추적 동의 창을 띄울 수 있습니다. [AppTrackingTransparency API 가이드 보기](https://developer.apple.com/documentation/apptrackingtransparency)

```swift
import AppTrackingTransparency

if #available(iOS 14, *) {
    ATTrackingManager.requestTrackingAuthorization { status in
                // ...
    }
 }
```

또는 SDK 가 제공하는 API 를 사용하여 앱 추적동의 창을 띄울 수 있습니다. (앱이 active 되는 시점에 맞추어 앱 추적동의 창을 띄워줍니다.)

```swift
import TnkRwdSdk2

TnkAlerts.showATTPopup(viewController,
                       agreeAction: {
                           // 사용자 동의함
                       },
                       denyAction:{
                           // 동의하지 않음
                       })

```

### Tnk 객체 초기화

SDK 사용을 위해서는 사전에 APP-ID 값을 발급 받으셔야합니다.  APP-ID 값은 [Tnk 사이트](https://tnkfactory.com) 에서 발급 받으 실 수 있습니다. APP-ID 값을 발급 받으셨다면 이 값을 사용하여 TnkSession 객체가 초기화되어야합니다. 이를 위해서는 2가지 방법이 존재합니다. 아래 2가지 방법 중 하나를 선택하시어 진행하시면 됩니다.

#### 초기화 API 호출하기

SDK 가 사용되기 전에 (일반적으로는 Application Delegate 의 applicationDidFinishLaunchingWithOption 메소드 내) 아래와 같이 초기화 로직을 넣습니다. 실제 APP-ID 값을 아래 로직의 your-app-id-from-tnk-site 부분에 넣어주어야합니다.

```swift
// Swift
import TnkRwdSdk2

TnkSession.initInstance(appId: "your-app-id-from-tnk-site")

```
#### info.plist 파일에 등록하기

XCode 프로젝트의 info.plist 파일내에 아래와 같이 `tnkad_app_id` 항목을 추가하고 APP-ID 값을 설정합니다. 이곳에 설정해두면 TnkSession 객체가 처음 사용되는 시점에 해당 APP-ID 값을 사용하여 자동으로 초기화됩니다.

<이미지>

## 2. 오퍼월 띄우기
### 유저 식별값 설정

오퍼월을 띄우기 위해서는 우선 앱내에서 사용자를 식별할 수 있는 값을 SDK 에 설정하여야합니다. 사용자 식별값은 일반적으로 로그인 ID 와 같은 값이 사용됩니다. 만약 사용자 식별값이 전화번호나 이메일등 개인 정보에 해당된다면 SHA256 과 같은 해쉬함수나 암호화 함수를 사용하여 주실것을 권장합니다.

사용자 식별값을 설정하지 않는 경우에는 오퍼월에는 광고가 출력되지 않습니다. 또한 사용자가 포인트 적립시 개발사의 서버로 호출하는 callback 내에 사용자 식별값이 같이 전달되므로 반드시 사용자 식별값을 설정하셔야합니다.

아래와 같이 호출하시어 사용자 식별값을 설정해주세요.

```swift
// Swift
import TnkRwdSdk2

TnkSession.sharedInstance()?.setUserName("<사용자 식별값>")

```

### AdOfferwallViewController 

오퍼월을 띄우는 가장 쉬운 방법은 **AdOfferwallViewController** 를 사용하는 것입니다.  AdOfferwallViewController 는 일반적인 UIViewController 와 동일한 방법으로 사용하실 수 있습니다. 아래의 예시는 AdOfferwallViewController 를 UINavigationController 에 추가하여 Modal 형태로 띄우는 예시입니다.

```swift
// Swift
import TnkRwdSdk2

func showOfferwall() {
    let vc = AdOfferwallViewController()
    vc.title = "TEST Offerwall"
        
    let navController = UINavigationController(rootViewController: vc)
    navController.modalPresentationStyle = .fullScreen
    navController.navigationBar.titleTextAttributes = [.foregroundColor: UIColor.black]

    self.present(navController, animated: true)
}

```
<오퍼월 이미지>
