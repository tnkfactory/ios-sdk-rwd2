## AdListItemView Classes

SDK 가 제공하는 전체 AdListItemView 클래스들은 아래와 같습니다.

```swift
// UICollectionViewCell
//  |
// AdListItemView
//  |
//  |-- IconOnlyAdListItemView
//  |
//  |-- BannerItemView
//  |
//  |-- CpsSearchItemView
//  |
//  |-- BaseAdListItemView
//       |
//       |-- BaseAdListItemViewInternal
//            |
//            |-- DefaultAdListItemView
//            |
//            |-- RightIconAdListItemView
//            |
//            |-- FeedAdListItemView
//            |
//            |-- BaseCpsItemView
//                 |
//                 |-- CpsBoxItemView
//                 |
//                 |-- CpsListItemView
//                 |
//                 |-- CpsFeedItemView
```

## Layout Classes

SDK 가 제공하는 전체 Layout 클래스들은 아래와 같습니다. AdListItemViewLayout 들을 상속 관계로 표시하였으며 옆의 괄호안에 적용 가능한 AdListItemView 클래스를 표시하였습니다.

```swift
// AdListItemViewLayout (DefaultAdListItemView, RightIconAdListItemView)
//  |
//  |-- RoundAdListItemViewLayout (DefaultAdListItemView, RightIconAdListItemView)
//  |    |
//  |    |-- RoundAdItemPageViewLayout (DefaultAdListItemView, RightIconAdListItemView)
//  |
//  |-- FeedAdItemScrollViewLayout (FeedAdListItemView)
//  |
//  |-- FeedAdItemLargeViewLayout (FeedAdListItemView)
//  |
//  |-- FeedAdItemPageViewLayout (FeedAdListItemView)
//  |
//  |-- BannerItemViewLayout
//  |    |
//  |    |-- BannerItemLargeViewLayout (BannerItemView)
//  |    |
//  |    |-- BannerItemListViewLaout (BannerItemView)
//  |
//  |-- IconOnlyAdItemScrollViewLayout (IconOnlyAdListItemView)
//  |
//  |-- NoAdListAdItemViewLayout (DefaultAdListItemView)
//  |
//  |-- CpsSearchItemViewLayout (CpsSearchItemView)
//  |
//  |-- CpsItemViewLayout
//       |
//       |-- CpsListItemViewLayout
//       |    |
//       |    |-- CpsBoxItemViewLayout (CpsBoxItemView)
//       |         |
//       |         |-- CpsBoxItemScrollViewLayout (CpsBoxItemView)
//       |         |
//       |         |-- NoCpsItemViewLayout (CpsBoxItemView)
//       |
//       |-- CpsItemPageViewLayout
//       |    |
//       |    |-- CpsListItemPageViewLayout (CpsListItemView)
//       |    |
//       |    |-- CpsBoxItemPageViewLayout (CpsBoxItemView)
//       |         |
//       |         |-- CpsBoxItemPageGrayLayout (CpsBoxItemView)
//       |
//       |-- CpsFeedItemViewLayout (CpsFeedItemView)
```

## 기본 레이아웃 설정

SDK 는 초기화시 아래와 같이 기본 Layout 을 설정합니다.

```swift
    // 배너 viewLayout
    registerItemViewLayout(type: .topbanner, viewClass: BannerItemView.self, viewLayout: BannerItemLargeViewLayout())
    registerItemViewLayout(type: .bottombanner, viewClass: BannerItemView.self, viewLayout: BannerItemLargeViewLayout())
    registerItemViewLayout(type: .listbanner, viewClass: BannerItemView.self, viewLayout: BannerItemListViewLayout())
        
    // 일반 광고 viewLayout
    registerItemViewLayout(type: .normal, viewClass: DefaultAdListItemView.self, viewLayout: AdListItemViewLayout())
    registerItemViewLayout(type: .promotion, viewClass: FeedAdListItemView.self, viewLayout: FeedAdItemPageViewLayout())
    registerItemViewLayout(type: .newapps, viewClass: RightIconAdListItemView.self, viewLayout: RoundAdItemPageViewLayout())
    registerItemViewLayout(type: .suggest, viewClass: FeedAdListItemView.self, viewLayout: FeedAdItemScrollViewLayout())
    registerItemViewLayout(type: .multi, viewClass: IconOnlyAdListItemView.self, viewLayout: IconOnlyAdItemScrollViewLayout())
        
    // 구매형 viewLayout
    registerItemViewLayout(type: .cpslist, viewClass: CpsBoxItemView.self, viewLayout: CpsBoxItemViewLayout())
    registerItemViewLayout(type: .favorite, viewClass: CpsBoxItemView.self, viewLayout: CpsBoxItemScrollViewLayout())
    registerItemViewLayout(type: .popular, viewClass: CpsListItemView.self, viewLayout: CpsListItemPageViewLayout())
    registerItemViewLayout(type: .reward, viewClass: CpsListItemView.self, viewLayout: CpsListItemPageViewLayout())
    registerItemViewLayout(type: .newitem, viewClass: CpsBoxItemView.self, viewLayout: CpsBoxItemPageGrayLayout())
    registerItemViewLayout(type: .recommend, viewClass: CpsBoxItemView.self, viewLayout: CpsBoxItemScrollViewLayout())
    registerItemViewLayout(type: .search, viewClass: CpsSearchItemView.self, viewLayout: CpsSearchItemViewLayout())
    registerItemViewLayout(type: .nocps, viewClass: CpsBoxItemView.self, viewLayout: NoCpsItemViewLayout())
        
    // 광고없을 때 & 뉴스 광고 viewLayout
    registerItemViewLayout(type: .noapps, viewClass: DefaultAdListItemView.self, viewLayout: NoAdListItemViewLayout())
    registerItemViewLayout(type: .newslist, viewClass: FeedAdListItemView.self, viewLayout: FeedAdItemLargeViewLayout())
```
