# Wordpress plugin to create Custom Post types




## Description
This is a wordpress custom post type plugin for the following post types.

* Awards
* Testimonials
* Specials
* Slideshows
* Galleries
* Announcements
* Media Clippings
* Newsletters
* Real Estate

## Settings.

### Settings -> CPT Settings
Custom Post type Enables

### Slideshows -> Settings
Add default slideshow dimensions.
Add default secondary slideshow dimensions.
Select Secondary defaults to Feature Image / Slideshow.

### Galleries -> Settings
Add Filters for galleries, specifically for feature gallery.

### Real Estate -> Settings
Price Units.
Area Units.
Custom menu.
Title for index.
Pre text for index.
Post text for index.
Call to action for display page.
Table Columns ( select columns, label and order).

##  Post Types

### Awards


### Testimonials

### Specials

### Slideshows

### Galleries

### Announcements

### Media Clippings

### Newsletters

### Real Estate



## Shortcodes

### [fgallery]

The **[fgallery]** shortcode accepts the following attribute.

| Attribute | Default | Description |
| --------- | ------- | ----------- |
| width     |  100px  | width of thumb |
| height    |  auto   | height of thumb |
| class     |         | adds class attribute |
| alt       |         | adds alt tag |
| thumb     |         | uses a different image as the thumb |
| group     |         | this adds group to gallery to link images to one group |

[fgallery alt="this is the alttext" thumb="absolute/path/to/image" width="150px" height="100%" class="my-class" ]<imc src="path/to/image" />[/fgallery]

### [page_gallery]

| Attribute | Description |
| --------- | ----------- |
| id        | The post id of the gallery post|
| feature   | This allows feature image or not default is false |
| filter    | This adds filters default is true |

[page_gallery id="344" feature="true" filter="false" ]


### [slick_carousel] and [slick_slide]

This carousel uses jquery plugin from Ken Wheeler at https://github.com/kenwheeler/slick

| Attribute | Default | Description |
| --------- | ------- | ----------- |
| id        | slick-carousel-default | selector id of  |
| accessibilty | true | |
| autoplay | false |  |
| infinite | false | |
| responsive |[{breakpoint: 1199, settings: { slidesToShow : 3}},{breakpoint: 989, settings : {slidesToShow : 2}},{breakpoint: 480, settings: {slidesToShow: 1}}] | |
| slidesperrow | 3| |
| slidestoshow | 3| |
| slidestoscroll | 1 | |
| speed | 300 | |
| dots | true | |
| arrows | true | |
| prevarrow | <a class="animiated-control-arrow control-arrow-prev "><span ></span></a> | |
| nextarrow | <a class="animiated-control-arrow control-arrow-next "><span ></span></a> | |

```
[slick_carousel id="my_slick_id" dots="false"]
  [slick_slide]<img src />[/slick_slide]
  [slick_slide]<img src />[/slick_slide]
  [slick_slide]<img src />[/slick_slide]
[/slick_carousel]

```
