Quantum Leap Info: Auto Layout Demo
============================

A small iOS application to demo Auto Layout that happens to reference a great television show (Quantum Leap).

This application was built to demo my Advanced Layouts with Auto Layout talk at the [Nashville Cocoaheads](https://twitter.com/nashcocoaheads) meetup. You can find the slides for that talk [here](http://groomsydev.org/advanced-layouts-with-auto-layout/index.html). The slides were exported using Keynote into an HTML presentation. To advance slides, click your mouse or use the arrow keys.

## Application Content
Each tab in this application represents a unique challenge that I have encountered while doing iOS development and utilizing Auto Layout.

### Synopsis
The synopsis tab is a simple `UIScrollView` that contains a title (`UILabel`), a press image (`UIImageView`), and a brief synopsis of the show (`UILabel`) below the press image. The tricky thing is laying this out in InterfaceBuilder without having a warning thrown regarding an ambiguous `contentSize` for your `UIScrollView`. It's very important to realize the constraints that need to be set to render the `UIScrollView` usable when you have more content than screen real estate. It's important to make use of "Remove at Runtime" constraints so that the layout is as desired when viewing in InterfaceBuilder and that, when running, the layout will be flexible enough to accommodate the content. Add a "greater than or equal to" constraint to ensure padding at the bottom (or sides if you have horizontally scrolling content).

### Quotes
The quotes tab is a `UITableViewController` that displays a few famous quotes from the television show and the characters who said the quotes. The tricky thing regarding this layout is that the quote length is variable and, unless you want a ridiculous looking table with misfitting cell heights, you'll need to dynamically change the height of the cells. This can be accomplished with proper Auto Layout constraints in your `UITableViewCell` (hint: Ensure you add your subviews to your `UITableViewCell`'s `contentView`) and by properly implementing the following two methods in your `UITableViewDelegate`:

* `- (CGFloat)tableView:(UITableView *)tableView estimatedHeightForRowAtIndexPath:(NSIndexPath *)indexPath`
* `- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath`

The key to using these methods is to calculate your heights as quickly and as efficiently as possible. Otherwise, you run the risk of a very slow, choppy scrolling experience.

### Notes
The notes tab is a simple form embedded in a `UIScrollView`. The tricky thing with this layout is to ensure that the form becomes scrollable when the keyboard is displayed. To keep the fields that will be covered by the keyboard visible, you must observe the `UIKeyboardWillShowNotification` and `UIKeyboardWillHideNotification` system notifications. You must then set the `contentInset` for your `UIScrollView` accordingly.

## Attribution
When first learning about dynamic cell heights for `UITableView`'s, I found this wonderful resource (which I occasionally reference): [Use Your Loaf: Table View Cells With Varying Row Heights](http://useyourloaf.com/blog/2014/02/14/table-view-cells-with-varying-row-heights.html)

Tab Bar Icons: [Pixeden: Tab Bar Icons iOS 7 Vol2](http://www.pixeden.com/media-icons/tab-bar-icons-ios-7-vol2)