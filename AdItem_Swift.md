## AdIem

서버에서 받은 광고 정보는 AdItem 객체에 담겨져있다. AdItem 객체는 AdListItemView 클래스의 setData() 함수로 전달되어 화면에 광고 내용을 출력하게 된다.
광고 목록 표시를 위하여 사용되는 AdItem 객체는 실제로는 AdListItem 객체이며 따라서 setData() 내에서는 전달 받은 AdItem 객체를 AdListItem 객체로 캐스팅하여 사용하여야한다.

아래는 AdItem 객체의 속성들이다.

```swift
public class BaseAdItem {
    public let appId:Int     // 광고 고유 ID
    public let actionId:Int  // 0: CPI, 1:CPE, 2: CPA, 3:CPV, 4:CPC, 5:CPS
    
    // ...
}

// AdInfoItem, AdBannerItem 의 공통 속성이다. 화면에 표시할 이미지 정보를 가지고 있다.
public class AdItem : BaseAdItem {
    
    public let appName:String     // 광고 타이틀
    public let iconUrl:String
    public let imageUrl:String?
    public let needAdid:Bool      // 광고 ID 필수 인 광고 여부
 
    // ...
}

// AdListItem, AdDetailItem 의 공통 속성이다.
// 광고유형, 지급포인트 등의 정보를 가지고 있다.
public class AdInfoItem : AdItem {
    
    public let osType:String
    public let pointUnit:String  // 포인트 단위
    public let corpDesc:String?
    public let appPackage:String?
    public let cmpnType:Int
    public var cmpnDesc:String  // cmpnType 값에 의하여 결정되는 캠페인 참여방식 문구
    public let pointValue:Int   // 지급되는 포인트 금액
    public let pointText:String // pointValue 를 포매팅한 문자열
    public var multiReward:Bool // 멀티 리워드 캠페인 여부
    public var favorite:Bool    // CPS 상품의 경우 즐겨찾기 여부
    
    // ...
}

// 광고 리스트 데이터의 각 row 를 담아두기 위한 클래스이다.
public class AdListItem : AdInfoItem {
    
    public let adType:Int
    public let filterId:Int
    public let needDetail:Bool
    public let originalPointAmount:Int    // 2배 이벤트시에 전달되는 원래 제공 포인트 금액
    
    public let multiJoin:Bool             // 현재 참여중인 멀티 리워드 캠페인인 경우 true
    
    // CPS 항목
    public let productPrice:Int           // 상품 가격
    public let originalProductPrice:Int   // 상품 할인 전 가격
    public let productNumber:Int          // 상품 고유 번호
    public let productPriceText:String    // 상품 가격을 포매팅한 문자열
    public let discountPercent:String     // 할인율
    
    public var state:AdState        // 현재 광고 상태 (아래 AdState 참고)

    // ...
}

public enum AdState : Int {
    case confirm = 0     // 설치확인 (설치형 광고)
    case normal = 1
    case paid = 2       // 적립된 광고
    case ended = 3      // 종료된 광고
    case disabled = 4   // 참여 불가 광고
    case tomorrow = 5   // 내일 구매 가능 (CPS)
}
```
