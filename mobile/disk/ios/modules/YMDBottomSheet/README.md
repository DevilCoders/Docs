# YMDBottomSheet

## Usage

```
    let viewController = SomeViewController()
    let navigationController = BottomSheetNavigationController(rootViewController: viewController)

    transitionDelegate = BottomSheetTransitioningDelegate(dismissalHandler: self)
    navigationController.transitioningDelegate = transitionDelegate
    navigationController.modalPresentationStyle = .custom

    present(navigationController, animated: true, completion: nil)
```

For details see Demo Application

## Author

Based on https://github.com/joomcode/BottomSheet#readme
