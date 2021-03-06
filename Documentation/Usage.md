# Usage
## SwipeMenuView
**1)** Integrate SwipeMenuViewController to your project as above

**2)** Import `SwipeMenuViewController` module

```swift
import SwipeMenuViewController
```

**3)** Add SwipeMenuView to `CustomViewController` , and set `dataSource`, `delegate`, and other options if you need

```swift
class CustomViewController: UIViewController {

    @IBOutlet weak var swipeMenuView: SwipeMenuView!

    override func viewDidLoad() {
        super.viewDidLoad()

        swipeMenuView.dataSource = self
        swipeMenuView.delegate = self

        let options: SwipeMenuViewOptions = .init()

        swipeMenuView.reloadData(options: options)
    }
}
```

**4)** Conform your `CustomViewController` to `SwipeMenuViewDelegate` to receive change events

```swift
extension CustomViewController: SwipeMenuViewDelegate {

    // MARK - SwipeMenuViewDelegate
    func swipeMenuView(_ swipeMenuView: SwipeMenuView, viewWillSetupAt currentIndex: Int) {
        // Codes
    }

    func swipeMenuView(_ swipeMenuView: SwipeMenuView, viewDidSetupAt currentIndex: Int) {
        // Codes
    }

    func swipeMenuView(_ swipeMenuView: SwipeMenuView, willChangeIndexFrom fromIndex: Int, to toIndex: Int) {
        // Codes
    }

    func swipeMenuView(_ swipeMenuView: SwipeMenuView, didChangeIndexFrom fromIndex: Int, to toIndex: Int) {
        // Codes
    }
}
```

**5)** Conform your `CustomViewController` to `SwipeMenuViewDataSource` to build the view

```swift
extension CustomViewController: SwipeMenuViewDataSource {

    //MARK - SwipeMenuViewDataSource
    func numberOfPages(in swipeMenuView: SwipeMenuView) -> Int {
        return array.count
    }

    func swipeMenuView(_ swipeMenuView: SwipeMenuView, titleForPageAt index: Int) -> String {
        return array[index]
    }

    func swipeMenuView(_ swipeMenuView: SwipeMenuView, viewControllerForPageAt index: Int) -> UIViewController {
        let vc = ContentViewController()
        return vc
    }
}
```

## SwipeMenuViewController
**1)** See SwipeMenuView process 1) ~ 2) to setup this SDK

**2)** Use `SwipeMenuViewController` classes

```swift
class CustomViewController: SwipeMenuViewController {}
```

**3)** Override `SwipeMenuViewDelegate` methods and `SwipeMenuViewDataSource` methods if you need.

```swift
extension CustomViewController {

    // MARK: - SwipeMenuViewDelegate
    override func swipeMenuView(_ swipeMenuView: SwipeMenuView, viewWillSetupAt currentIndex: Int) {
        // Codes
    }

    override func swipeMenuView(_ swipeMenuView: SwipeMenuView, viewDidSetupAt currentIndex: Int) {
        // Codes
    }

    override func swipeMenuView(_ swipeMenuView: SwipeMenuView, willChangeIndexFrom fromIndex: Int, to toIndex: Int) {
        // Codes
    }

    override func swipeMenuView(_ swipeMenuView: SwipeMenuView, didChangeIndexFrom fromIndex: Int, to toIndex: Int) {
        // Codes
    }

    // MARK - SwipeMenuViewDataSource
    override func numberOfPages(in swipeMenuView: SwipeMenuView) -> Int {
        return array.count
    }

    override func swipeMenuView(_ swipeMenuView: SwipeMenuView, titleForPageAt index: Int) -> String {
        return array[index]
    }

    override func swipeMenuView(_ swipeMenuView: SwipeMenuView, viewControllerForPageAt index: Int) -> UIViewController {
        let vc = ContentViewController()
        return vc
    }
}
```

## Methods
`SwipeMenuView` has the following methods.

```swift
// Reloads all `SwipeMenuView` item views with the dataSource and refreshes the display.
func reloadData(options: SwipeMenuViewOptions? = nil, isOrientationChange: Bool = false)

// Jump to the selected page.
func jump(to index: Int, animated: Bool)

// Notify changing orientaion to `SwipeMenuView` before it.
func willChangeOrientation()
```

`TabView` has the following methods.
```swift

/// Reloads all `TabView` item views with the dataSource and refreshes the display.
public func reloadData(options: SwipeMenuViewOptions.TabView? = nil, default defaultIndex: Int? = nil)
```

## Protocols
`SwipeMenuViewDataSource` and `SwipeMenuViewDelegate` has the following methods.

```swift
// Return the number of pages in `SwipeMenuView`.
func numberOfPages(in swipeMenuView: SwipeMenuView) -> Int

// Return strings to be displayed at the specified tag in `SwipeMenuView`.
func swipeMenuView(_ swipeMenuView: SwipeMenuView, titleForPageAt index: Int) -> String

// Return a ViewController to be displayed at the specified page in `SwipeMenuView`.
func swipeMenuView(_ swipeMenuView: SwipeMenuView, viewControllerForPageAt index: Int) -> UIViewController

/// Called before setup self.
func swipeMenuView(_ swipeMenuView: SwipeMenuView, viewWillSetupAt currentIndex: Int)

/// Called after setup self.
func swipeMenuView(_ swipeMenuView: SwipeMenuView, viewDidSetupAt currentIndex: Int)

// Called before swiping the page.
func swipeMenuView(_ swipeMenuView: SwipeMenuView, willChangeIndexFrom fromIndex: Int, to toIndex: Int)

// Called after swiping the page.
func swipeMenuView(_ swipeMenuView: SwipeMenuView, didChangeIndexFrom fromIndex: Int, to toIndex: Int)
```

## Properties
`SwipeMenuView` has the following properties.

```swift
// An object conforms `SwipeMenuViewDelegate`. Provide views to populate the `SwipeMenuView`.
open weak var delegate: SwipeMenuViewDelegate!

// An object conforms `SwipeMenuViewDataSource`. Provide views and respond to `SwipeMenuView` events.
open weak var dataSource: SwipeMenuDataSource!

// The index of the front page in `SwipeMenuView` (read only).
private(set) var currentIndex
```

`TabView` has the following properties.
```swift

// An object conforms `TabViewDelegate`. Provide views to populate the `TabView`.
open weak var tabViewDelegate: TabViewDelegate?

// An object conforms `TabViewDataSource`. Provide views and respond to `TabView` events.
open weak var dataSource: TabViewDataSource?
```

## Customization
`SwipeMenuView` is customizable by designated options property when calling `reloadData()` method.
Here are many properties of `SwipeMenuViewOptions` which you are able to customize it for your needs.

### TabView

```swift
// TabView height. Defaults to `44.0`.
public var height: CGFloat

// TabView side margin. Defaults to `0.0`.
public var margin: CGFloat

// TabView background color. Defaults to `.clear`.
public var backgroundColor: UIColor

// TabView clipsToBounds. Defaults to `true`.
public var clipsToBounds: Bool = true

// TabView style. Defaults to `.flexible`. Style type has [`.flexible` , `.segmented`].
public var style: Style

// TabView addition. Defaults to `.underline`. Addition type has [`.underline`, `.circle`, `.none`].
public var addition: Addition

// TabView adjust width or not. Defaults to `true`.
public var needsAdjustItemViewWidth: Bool

// Convert the text color of ItemView to selected text color by scroll rate of ContentScrollView. Defaults to `true`.
public var needsConvertTextColorRatio: Bool

// TabView enable safeAreaLayout. Defaults to `true`.
public var isSafeAreaEnabled: Bool

// TabView enable AdditionView swipe animation. Defaults to `true`.
public var isAnimationOnSwipeEnable: Bool
```

### ItemView

```swift
// ItemView width. Defaults to `100.0`.
public var width: CGFloat

// ItemView side margin. Defaults to `5.0`.
public var margin: CGFloat

// ItemView font. Defaults to `14 pt as bold SystemFont`.
public var font: UIFont

// ItemView clipsToBounds. Defaults to `true`.
public var clipsToBounds: Bool = true

// ItemView textColor. Defaults to `.lightGray`.
public var textColor: UIColor

// ItemView selected textColor. Defaults to `.black`.
public var selectedTextColor: UIColor
```

### AdditionView

```swift
// AdditionView height. Defaults to `2.0`.
public var height: CGFloat

// AdditionView padding. Defaults to `.zero`.
public var padding: UIEdgeInsets

// AdditionView backgroundColor. Defaults to `.black`.
public var backgroundColor: UIColor

// AdditionView animating duration. Defaults to `0.3`.
public var animationDuration: Double

// Underline style options.
public var underline = Underline()

// Circle style options.
public var circle = Circle()

// Circle style maskedCorner options. It helps to make specific corners rounded. Defaults to `nil`.
public var maskedCorners: CACornerMask? = nil
```

### ContentScrollView

```swift
// ContentScrollView backgroundColor. Defaults to `.clear`.
public var backgroundColor: UIColor

// ContentScrollView clipsToBounds. Defaults to `true`.
public var clipsToBounds: Bool = true

// ContentScrollView scroll enabled. Defaults to `true`.
public var isScrollEnabled: Bool

// ContentScrollView enable safeAreaLayout. Defaults to `true`.
public var isSafeAreaEnabled: Bool
```
