## AdListItemView.swift

```swift
import UIKit

// AdListItemView 내에서 발생하는 버튼 이벤트를 처리하기 위한 용도이다.
protocol AdItemDelegate : NSObjectProtocol {
    func didFavoriteItemSelected(_ appId:Int, isSelected:Bool) -> Bool  // 처리 성공여부
    func didButtonItemClicked(_ appId:Int, buttonId:Int)  // 1: search, 2: mymenu
}

// 광고 목록의 아이템 표시를 위한 최상위 클래스
// 하위 클래스가 구현해야할 메소드를 정의하였으며, 이미지 로딩 기능이 구현되어 있다.
// 매체사에서 커스마이징을 원할 경우 이 클래스의 하위 클래스를 구현한다.
public class AdListItemView : UICollectionViewCell {
    weak var adItemDelegate:AdItemDelegate?
    
    private var didLayout:Bool = false  // 내부 UI 구현이 완료되었는지 여부 저장용 (생성자에서 UI 구현을 하지 않고 applyLayout() 사용해서 구현함)
    
    private var useIconImage:Bool = true
    private var useFeedImage:Bool = false
    
    // View 가 표시하고 있는 광고를 식별하기 위하여 내부적으로 사용한다. (아이콘 이미지 로딩 후 적용여부를 판단하기 위한 용도이다.)
    var adItemKey:Int = 0
    
    override init(frame:CGRect) {
        super.init(frame:frame)
    }
    
    required init?(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    func applyViewLayout(_ viewLayout:AdListItemViewLayout) {
        if !didLayout {
            applyLayout(viewLayout)
        }
        
        didLayout = true
    }
    
    // UI 구성 요소들의 속성값과 LayoutConstraint 등의 설정을 구현한다.
    public func applyLayout(_ viewLayout:AdListItemViewLayout) {
        // 하위 클래스에서 applyLayout 구현시 이 함수를 먼저 호출해야한다.
        useIconImage = viewLayout.useIconImage
        useFeedImage = viewLayout.useFeedImage
        
        contentView.backgroundColor = viewLayout.itemBackgroundColor
        contentView.layer.cornerRadius = viewLayout.itemCornerRadius
        if viewLayout.itemStrokeWidth > 0 {
            contentView.layer.borderWidth = viewLayout.itemStrokeWidth
            contentView.layer.borderColor = viewLayout.itemStrokeColor.cgColor
        }
        contentView.clipsToBounds = true
        
        if let favoriteButton = getFavoriteButton() {
            // favorite 버튼 클릭 처리
            favoriteButton.addTarget(self, action: #selector(updateFavoriteButton(_:)), for: .touchUpInside)
        }
    }
    
    // row : indexPath.row
    // itemsPerPage: 페이지당 아이템 갯수
    // itemIndex : 섹션내에 표시되는 전체 아이템 중에서 몇번째 아이템인지 알려줌 (페이징 처리되는 경우 indexPath.row 값과는 다르다)
    // numberOfItems : 섹션 내에 표시되는 전체 아이템 갯수
    public func setData(_ adItem:AdItem?, row:Int, itemsPerPage:Int, itemIndex:Int, numberOfItems:Int) {
        // 하위 클래스에서 구현한다.
    }
    
    // 아이콘 이미지 표시 여부를 반환한다.
    public func useImageIcon() -> Bool {
        return useIconImage
    }
    
    public func setImageIcon(_ image:UIImage?) {
        getIconImageView()?.image = image
    }
    
    // 피드 이미지 표시 여부를 반환한다.
    public func useImageFeed() -> Bool {
        return useFeedImage
    }

    // 피드이미지 설정 함수이다. 하위 클래스에서 구현한다.
    public func setImageFeed(_ image:UIImage?) {
        getFeedImageView()?.image = image
    }
    
    //
    // MARK: 커스터마이징을 위한 UI 컨트롤의 Bind 함수들
    //
    
    public func getIconImageView() -> UIImageView? {
        return nil
    }
    
    public func getFeedImageView() -> UIImageView? {
        return nil
    }
    
    public func getTitleLabel() -> UILabel? {
        return nil
    }
    
    public func getDescLabel() -> UILabel? {
        return nil
    }
    
    public func getPointAmountLabel() -> UILabel? {
        return nil
    }

    public func getPointUnitLabel() -> UILabel? {
        return nil
    }
    
    public func getPointImageView() -> UIImageView? {
        return nil
    }
    
    public func getDividerLineView() -> UIView? {
        return nil
    }
    
    // CPS 용 추가 컨트롤
    
    public func getProductPriceLabel() -> UILabel? {
        return nil
    }

    public func getDiscountRateLabel() -> UILabel? {
        return nil
    }
    
    public func getFavoriteButton() -> UIButton? {
        return nil
    }
    
    // MARK: Favorite Button API 호출
    @objc
    final func updateFavoriteButton(_ sender:UIButton) {
        let isSelected = !sender.isSelected
        if adItemDelegate?.didFavoriteItemSelected(adItemKey, isSelected: isSelected) == true {
            sender.isSelected = isSelected
        }
    }
    
    // MARK: Image Loading
    
    final func loadImageIcon(appId:Int, imageUrl:String) {
        
        TnkImageCache.shared.readImage(appId:appId, url: imageUrl) { (appId, image) in
            
            if appId == self.adItemKey {
                // 이미지 로딩이 완료되었을 때와 처음 요청할때의 appId가 같은 경우에만 이미지를 반영한다.
                self.setImageIcon(image)
            }
        }
    }
    
    final func loadImageFeed(appId:Int, imageUrl:String) {
        
        TnkImageCache.shared.readImage(appId:appId, url: imageUrl) { (appId, image) in
            
            if appId == self.adItemKey {
                // 이미지 로딩이 완료되었을 때와 처음 요청할때의 appId가 같은 경우에만 이미지를 반영한다.
                self.setImageFeed(image)
            }
        }
    }
    
}
```
