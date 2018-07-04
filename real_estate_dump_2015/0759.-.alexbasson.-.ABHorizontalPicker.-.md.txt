ABHorizontalPicker
==================

A horizontal picker in the vein of UIPickerView, using UICollectionViews.

Use Cases
---------

A horizontal picker has one huge advantage over the standard UIPickerView, and that is screen real estate.  UIPickerViews take up an enormous amount of vertical space, and although that's less of an issue on the iPhone 5 than on previous iPhones, UIPickerViews can still take up as much as half of the screen.

ABHorizontalPickerView preserves vertical screen real estate.  The developer has complete control over the vertical size of each component and can tailor that size to fit the UI needs for each picker individually.  A picker with two components, each of which is 44 points high, takes up only 94 points of vertical space; this is contrasted with a UIPickerView, which by default takes up 216 points of vertical space.

On the other hand, ABHorizontalPickerView is best used when the data being picked is short. Numbers and letters work well; day or month names work poorly.

Features
--------

ABHorizontalPickerView follows the pattern of UIPickerView of having a data source and a delegate, with method signatures closely corresponding to those of UIPickerView. Where appropriate, the word "row" has been replaced with the word "column", but otherwise the method signatures are nearly identical. This allows developers to use ABHorizontalPickerView without having to learn a whole new set of methods.

In addition, ABHorizontalPickerView allows the developer to customize the selection indicator color, which some developers might choose to do for aesthetic or branding reasons.
