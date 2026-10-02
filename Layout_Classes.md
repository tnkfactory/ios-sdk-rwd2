## AdListItemView Classes

SDK 가 제공하는 전체 AdListItemView 클래스들은 아래와 같습니다.

```swift
// UICollectionViewCell
//  |
// AdListItemView
//  |
//  |-- IconOnlyAdListItemView
//  |
//  |-- MultiRewardAdListItemView
//  |
//  |-- FeedOnlyAdListItemView
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
//                 |
//                 |-- CpsRightIconListItemView
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
//  |    |
//  |    |-- SingleTitleFeedAdItemLargeViewLayout (FeedAdListItemView)
//  |    |
//  |    |-- FeedOnlyAdItemLargeViewLayout (FeedOnlyAdListItemView)
//  |
//  |-- FeedAdItemPageViewLayout (FeedAdListItemView)
//  |
//  |-- BannerItemViewLayout
//  |    |
//  |    |-- BannerItemCarouselLayout (BannerItemView)
//  |    |
//  |    |-- BannerItemLargeViewLayout (BannerItemView)
//  |    |
//  |    |-- BannerItemListViewLayout (BannerItemView)
//  |
//  |-- IconOnlyAdItemScrollViewLayout (IconOnlyAdListItemView, MultiRewardAdListItemView)
//  |
//  |-- ADTopRecommendItemListLayout (DefaultAdListItemView)
//  |
//  |-- EmptyListItemLayout (DefaultAdListItemView)
//  |
//  |-- PlacementBaseViewLayout
//  |    |
//  |    |-- PlacementFeedViewLayout (FeedAdListItemView)
//  |    |    |
//  |    |    |-- PlacementFeedOnlyViewLayout (FeedOnlyAdListItemView)
//  |    |
//  |    |-- PlacementFixedSizeFeedViewLayout (FeedAdListItemView)
//  |    |
//  |    |-- PlacementIconViewLayout (IconOnlyAdListItemView)
//  |    |
//  |    |-- PlacementListViewLayout (DefaultAdListItemView)
//  |
//  |-- NoAdListItemViewLayout (DefaultAdListItemView)
//  |
//  |-- CpsSearchItemViewLayout (CpsSearchItemView)
//  |
//  |-- CpsItemViewLayout
//       |
//       |-- CpsListItemViewLayout
//       |    |
//       |    |-- CpsTopRecommendItemListLayout (CpsListItemView)
//       |    |
//       |    |-- CpsBoxItemViewLayout (CpsBoxItemView)
//       |         |
//       |         |-- CpsBoxItemScrollViewLayout (CpsBoxItemView)
//       |         |
//       |         |-- NoCpsItemViewLayout (CpsBoxItemView)
//       |
//       |-- CpsItemPageViewLayout
//       |    |
//       |    |-- CpsGrayRoundListItemPageViewLayout (CpsRightIconListItemView)
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
    registerItemViewLayout(type: .topbanner, viewClass: BannerItemView.self, viewLayout: BannerItemCarouselLayout())
    registerItemViewLayout(type: .bottombanner, viewClass: BannerItemView.self, viewLayout: BannerItemLargeViewLayout())
    registerItemViewLayout(type: .listbanner, viewClass: BannerItemView.self, viewLayout: BannerItemListViewLayout())
        
    // 일반 광고 viewLayout
    registerItemViewLayout(type: .normal, viewClass: DefaultAdListItemView.self, viewLayout: AdListItemViewLayout())
    registerItemViewLayout(type: .promotion, viewClass: FeedAdListItemView.self, viewLayout: FeedAdItemPageViewLayout())
    registerItemViewLayout(type: .newapps, viewClass: RightIconAdListItemView.self, viewLayout: RoundAdItemPageViewLayout())
    registerItemViewLayout(type: .suggest, viewClass: FeedAdListItemView.self, viewLayout: FeedAdItemScrollViewLayout())
    registerItemViewLayout(type: .multi, viewClass: MultiRewardAdListItemView.self, viewLayout: IconOnlyAdItemScrollViewLayout())
        
    // 퀴즈 viewLayout (.quiz_list 는 SDK 내부 레이아웃을 사용합니다)
    registerItemViewLayout(type: .quiz_feed, viewClass: FeedAdListItemView.self, viewLayout: SingleTitleFeedAdItemLargeViewLayout())
        
    // 구매형 viewLayout
    registerItemViewLayout(type: .cpslist, viewClass: CpsBoxItemView.self, viewLayout: CpsBoxItemViewLayout())
    registerItemViewLayout(type: .favorite, viewClass: CpsBoxItemView.self, viewLayout: CpsBoxItemScrollViewLayout())
    registerItemViewLayout(type: .popular, viewClass: CpsListItemView.self, viewLayout: CpsListItemPageViewLayout())
    registerItemViewLayout(type: .reward, viewClass: CpsListItemView.self, viewLayout: CpsListItemPageViewLayout())
    registerItemViewLayout(type: .newitem, viewClass: CpsRightIconListItemView.self, viewLayout: CpsGrayRoundListItemPageViewLayout())
    registerItemViewLayout(type: .cps_newitem_B, viewClass: CpsRightIconListItemView.self, viewLayout: CpsGrayRoundListItemPageViewLayout())
    registerItemViewLayout(type: .recommend, viewClass: CpsBoxItemView.self, viewLayout: CpsBoxItemScrollViewLayout())
    registerItemViewLayout(type: .search, viewClass: CpsSearchItemView.self, viewLayout: CpsSearchItemViewLayout())
    registerItemViewLayout(type: .nocps, viewClass: CpsBoxItemView.self, viewLayout: NoCpsItemViewLayout())
        
    // 상단 추천 영역 viewLayout
    registerItemViewLayout(type: .top_recommend_ad, viewClass: DefaultAdListItemView.self, viewLayout: ADTopRecommendItemListLayout())
    registerItemViewLayout(type: .top_recommend_cps, viewClass: CpsListItemView.self, viewLayout: CpsTopRecommendItemListLayout())
        
    // 광고없을 때 & 뉴스 광고 viewLayout
    registerItemViewLayout(type: .noapps, viewClass: DefaultAdListItemView.self, viewLayout: NoAdListItemViewLayout())
    registerItemViewLayout(type: .empty, viewClass: DefaultAdListItemView.self, viewLayout: EmptyListItemLayout())
    registerItemViewLayout(type: .newslist, viewClass: FeedAdListItemView.self, viewLayout: FeedAdItemLargeViewLayout())
```
