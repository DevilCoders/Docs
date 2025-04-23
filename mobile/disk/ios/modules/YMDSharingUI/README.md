# YMDSharingUI

## Requirements

    To create a controller, you need to implement a ViewModel that meets its requirements

## Usage

    All public controllers support showing in BottomSheet and Popover.
    They can also be shown as stand-alone screens,
    or in DiskSharingPopoverController or DiskSharingNavigationController containers

```
    let controller = DiskSharingViewController<YouViewModel>()
    controller.viewModel = YouViewModel()
        
    let containerVC = DiskSharingNavigationController(rootViewController: controller)
    containerVC.transitioningDelegate = BottomSheetTransitioningDelegate(dismissalHandler: self)
    containerVC.modalPresentationStyle = .custom
    
    present(containerVC, animated: true)
```

For details see Demo Application
