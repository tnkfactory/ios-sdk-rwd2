## LayoutType

```swift
public enum LayoutType : Int {
    // 일반광고
    case normal = 0
    case promotion = 1  // 소진 큐레이션
    case newapps = 2    // 신규 큐레이션
    case suggest = 3    // 운영자 등록 큐레이션
    case multi = 4      // 참여중인 멀티리워드 캠페인
    case noapps = 9     // 광고 없을때 SDK가 생성하는 추천 광고 큐레이션
    
    // 구매형
    case cpslist = 10       // CPS 기본 목록
    case favorite = 11      // 관심상품, 최근 구매
    case popular = 12       // 구매형 인기상품
    case reward = 13        // 구매형 리워드 가성비
    case newitem = 14       // 구매형 신규상품
    case recommend = 15     // 구매형 운영자 등록
    case search = 16        // 검색 + CPS My메뉴 아이템
    case nocps = 19         // CPS 상품 없을때 SDK가 생성하는 추천 광고 큐레이션
    
    // 배너
    case topbanner = 21     // 상단 배너
    case listbanner = 22    // 목록 배너
    case bottombanner = 23  // 하단 배너
    
    // 컨텐츠
    case newslist = 31      // 뉴스(컨텐츠) 기본 목록
}
```
