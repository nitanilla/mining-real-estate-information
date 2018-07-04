[![CircleCI build badge](https://circleci.com/gh/trms/carousel-api-php.svg?style=shield&circle-token=:circle-token)](https://circleci.com/gh/trms/carousel-api-php.svg?style=shield&circle-token=:circle-token)
[![License](https://poser.pugx.org/trms/carousel/license)](https://packagist.org/packages/trms/carousel)
[![Total Downloads](https://poser.pugx.org/trms/carousel/downloads)](https://packagist.org/packages/trms/carousel)
[![Latest Stable Version](https://poser.pugx.org/trms/carousel/version)](https://packagist.org/packages/trms/carousel)
[![Code Climate](https://img.shields.io/codeclimate/github/trms/carousel-api-php.svg)]()

# PHP Package for the Carousel API
This package is designed to be a fluent interface for Tightrope Media Systems' Carousel API.  For more information on TRMS and the Carousel software please visit [www.trms.com](https://www.trms.com).

## Carousel API
This package requires ownership of Carousel software version 7 or greater. General information about the Carousel API can be found on your carousel server at `your_carousel_server/carouselapi`.

## Package Installation
This package should be installed with composer and requires PHP 7+
```bash
composer install trms/carousel
```
## [Examples](#basic-usage-examples)

## [Servers & Requests](#servers-and-requests)
[The Server Instance](#api)

[Model Requests](#modelrequest)

[File Upload Requests](#fileuploadrequest)

[Bulletin Order Requests](#bulletinorderrequest)
## [Carousel Models](#models)
[Templates](#template)

[Bulletins](#bulletin)

[Bulletin & Template Blocks](#bulletinblock)

[Groups](#group)

[Media](#media)

[Zones](#zone)

[Tags](#tags)

[Bulletin Sorting](#bulletin-sorting)

## [Thrown Exceptions](#exceptions)

## Basic Usage Examples

### Creating a server instance
Server methods that return more than one object will return a [collection](https://github.com/tightenco/collect), which can be treated like an array.
```php
use TRMS\Carousel\Server\API;

$server = new Server();
$server->connect('http://my_carousel_server.com', 'username', 'password');
```

### Requesting Carousel Resources
All of the requests for Carousel resources are created by instantiating a `ModelRequest` with the appropriate `Model` class name and passing that to the server's `get` method.  Passing an array of parameters to the `ModelRequest` is also important so that your query is limited to the items you want to get.

For example, to get a set of bulletins in a given zone:
```php
use TRMS\Carousel\Requests\ModelRequest;
use TRMS\Carousel\Models\Bulletin;

$request = new ModelRequest(Bulletin::class, ['ZoneID'=>'5','IsDeleted'=>false]);
$bulletins = $server->get($request);
```

### Saving a Resource
New or existing resources can be saved by passing them to the `save` method on a server instance.

```php
use TRMS\Carousel\Models\BulletinTag;

$new_tag = new BulletinTag(['TagName'=>'My New Tag']);
$server->save($new_tag);
```

### Creating a Bulletin From A Template
Usually you will be creating new bulletins from existing templates.  More information on [Templates](#template) can be found below. Please note that **all bulletins must belong to a group** and this group must be created and related to the bulletin first when saving a newly created bulletin. More information on this can be found in the section on [Bulletins](#bulletin) below.
```php
use TRMS\Carousel\Requests\ModelRequest;
use TRMS\Carousel\Models\Bulletin;
use TRMS\Carousel\Models\Group;
use TRMS\Carousel\Models\Template;


$templates = $server->get(new ModelRequest(Template::class, ['ZoneID'=>'5','IsDeleted'=>false]));
$template = $templates->first(); // the server returns a Laravel Collection.
$bulletin = Bulletin::fromTemplate($templates->first());
// here you would likely modify the bulletin's 'Blocks' to alter content
$group = new Group(['ZoneID'=>'5']);
$server->save($group);
$bulletin->setGroup($group);
$server->save($bulletin);
```

### Creating Content from File Uploads
You can create new Media and Bulletins by uploading a file to the Carousel Server.  This is done by instantiating a `FileUploadRequest` with the appropriate `Model` class name and an array of parameters passed to the request.  `ZoneID` is required.  You will then add the files you wish to upload by chaining `addFile` methods and then pass the request to the server's `upload` method.  This will return an array of models, one for each file that was added.
```php
use TRMS\Carousel\Request\FileUploadRequest;
use TRMS\Carousel\Model\Media;

$request = new FileUploadRequest(Media::class, ['ZoneID'=>'5']);
$request->addFile('/path/to/local/file.jpg')->addFile('http://path/to/remote/file');

$media = $server->upload($request);
```

# Entities

## Servers and Requests
### API
`TRMS\Carousel\Server\API`

This represents the Carousel server itself
#### Methods
|Method|Parameters|Returns|Description|
|------|----------|-------|-----------|
|connect|server origin, username, password|self - chainable|Connect to the server with a url and authentication information.  be sure to include the scheme (ie:http://)|
|whoAmI|none|User Object|Gets the currently connected user.|
|get|ModelRequest|Model or Collection of Models|Get a specified resource or set of resources from the server|
|save|Model|null|Save a model|
|delete|Model|null|Delete a model.  Note that most resources in Carousel are soft deleted on the server and the result will be the property `IsDeleted` will be set to true.|
|upload|FileUploadRequest|Collection of Models|Upload a file or set of files to the server to create content with.|


### ModelRequest
`TRMS\Carousel\Requests\ModelRequest`

Model requests are used to get models from the server.
#### Methods
|Method|Parameters|Returns|Description|
|------|----------|-------|-----------|
|constructor|Model ClassName, associative array|Request Object|Pass this the class name of the Model you would like to retrieve (ie: Bulletin::class) and an associative array of values to filter the request with. (ie: either [id=>'some_id_value'] or ['ZoneID'=>'5',IsDeleted=>false])|

### FileUploadRequest
`TRMS\Carousel\Requests\FileUploadRequest`

File upload requests are used to post images video or audio to the server in order to create content with it either as Media assets or as Bulletins.
#### Methods
|Method|Parameters|Returns|Description|
|------|----------|-------|-----------|
|constructor|Model ClassName, associative array|Request Object|Pass this the class name of the Model you would like to retrieve (ie: Bulletin::class) and an associative array that determines the values to create the resource with. (ie: ['ZoneID'=>'5']) (currently only ZoneID is supported and its also required)|
|addFile|string|self - chainable|The URL or file path of the file to upload to the server|

### BulletinOrderRequest
`TRMS\Carousel\Requests\BulletinOrderRequest`

Bulletin order requests are used to get the Group/Bulletin order for a given Zone.  A ZoneID is required as a parameter when creating the request. For more information see the section on [bulletin sorting](#bulletin-sorting) below.
#### Methods
|Method|Parameters|Returns|Description|
|------|----------|-------|-----------|
|constructor|associative array|Request Object|Pass this an associative array of values to filter the request with. (ie:['ZoneID'=>'5'])|

## Models
|Method|Parameters|Returns|Description|
|------|----------|-------|-----------|
|constructor|associative array|self|Constructor for the class, properties passed to it will be used to define the Model.|
|save|none|none|This is a convenience method for saving previously persisted models. For newly instantiated models this function will throw a `CarouselModelException`.  Use the API's `save` method to save new models.|
|delete|none|none|This is a convenience method for deleting previously persisted models. For newly instantiated models this function will throw a `CarouselModelException`.|
### Bulletin
`TRMS\Carousel\Models\Bulletin`

A Bulletin is a piece of content displayed in Carousel.  The closest analogy would be a slide in a power point deck.
#### Methods
|Method|Parameters|Returns|Description|
|------|----------|-------|-----------|
|fromTemplate (static)|Template Object|Bulletin Object|Create a new unsaved bulletin from a template.|
|resolvePartial|none|none|Resolves partial bulletins by getting them by id from the server.  See the property `PartialBulletin` for more information.  This function is called when trying to save partial bulletins.|
|**Relationships**|
|setBackground|Media Object|self - chainable|Sets the background Media to be used in this model.|
|getBackground|none|Media Object|Gets the related background Media model.|
|addBlock|Block Object|self - chainable|Add a Block relationship to the model.|
|removeBlock|Block Object|self - chainable|Remove a Block relationship from the model.|
|setGroup|Group Object|self - chainable|Sets the Group for this bulletin|
|getGroup|none|Group Object|Gets the group for this bulletin|
|addTag|Tag Object|self - chainable|Add a Tag relationship to the model.|
|removeTag|Tag Object|self - chainable|Remove a Tag relationship from the model.|
|setUser|User Object|self - chainable|Sets the User to be used in this model.|
|getUser|none|User Object|Gets the related User model.|
|**Scheduling**|
|resetScheduled|none|self - chainable|Resets the `DateTimeOn` and `DateTimeOff` to today and `IsScheduled` to false.|
|setSchedule|DateTime, DateTime|self - chainable|Sets the `DateTimeOn` and `DateTimeOff` properties|
|setDateTimeOn|DateTime|self - chainable|Sets the `DateTimeOn` property.|
|setDateTimeOff|DateTime|self - chainable|Sets the `DateTimeOff` property.|
|resetCycleTimes|none|self - chainable|Resets the `CycleTimeOn` and `CycleTimeOff` to be 'on all day'.|
|setCycleTimes|DateTime, DateTime|self - chainable|Sets the `CycleTimeOn` and `CycleTimeOff` properties.|
|setCycleTimeOn|DateTime|self - chainable|Sets the `CycleTimeOn` property.|
|setCycleTimeOff|DateTime|self - chainable|Sets the `CycleTimeOff` property.|
|setDaysOnAll|boolean (default true)|self - chainable|Sets display property for all days.|
|setDaysOnWeekend|boolean (default true)|self - chainable|Sets display property for weekends.|
|setDaysOnWeekdays|boolean (default true)|self - chainable|Sets display property for weekdays.|
|setDaysOn{Dayname}|boolean (default true)|self - chainable|Sets display property for a single day of the week (ie: `setDaysOnSaturday()`).|
#### Properties
|Property|type|Description|
|--------|----|-----------|
|id|string|This is set by the server and not editable.|
|Blocks|array|An array of Block objects|
|Description|string|The description of the Bulletin|
|DwellTime|int|How long the bulletin displays each rotation.|
|UseSystemDwellTime|boolean|Should the system decide how long this bulletin displays each rotation, if false use the defined dwell time.|
|IsAlert|boolean|Is this Bulletin an alert bulletin? Alerts will override any non-alert content in a zone.|
|IsDeleted|boolean|Soft deletion property, soft deleted bulletins will be cleaned up and permanently deleted after a time.|
|IsScheduled|boolean|Does this bulletin respect the DateTimeOn and DateTimeOff values|
|DateTimeOn|string|The date and time the bulletin will begin playing. (there are helper methods for setting this value)|
|DateTimeOff|string|The date and time the bulletin will stop playing. (there are helper methods for setting this value)|
|CycleTimeOn|string|The time the bulletin will begin playing each day it is scheduled Only the time portion of this is used by the server. (there are helper methods for setting this value)|
|CycleTimeOff|string|The time the bulletin will stop playing each day it is scheduled Only the time portion of this is used by the server. (there are helper methods for setting this value)|
|WeekdayOnOff|int|A bit-field representation of the days of the week that this bulletin will play during its schedule. (there are helper methods for setting this value)|
|WeekdayOnOffDescription|string (read only)|A human readable representation of the WeekdayOnOff value.|
|IsRepeating|boolean|Does this bulletin repeat playback every Nth bulletin.|
|RepeatInterval|int|How often a repeating bulletin repeats.|
|LastUpdate|string|Date and time of the last rendering of this bulletin.|
|LastError|string|The last error encountered when rendering this bulletin|
|PartialBulletin|boolean (read only)|Getting bulletins from the server via any query other than `id` will result in a partial bulletin.  Partial bulletins do not contain some relationship data including Blocks and many of the properties for dynamic bulletins, if you need to act on these properties call `resolvePartial()` in order to get those properties from the server.|
|Status|enumerable (read only)|One of the following values: Current, Queued, Hold, Old, Saved, Current-Null (no dynamic content), Current-Error|
|Tags|array |An Array of Tag Objects|
|TrackImpressions|boolean|Should the service track each time this bulletin is played on a player|
|ImpressionCount|int|The number of times a tracked bulletin has played on a player|
|Type|enumerable|The type of bulletin, Bulletins created from templates are `Standard`.  There are several dynamic Bulletin types that all have their own set of properties related to the dynamic content.  (future updates may outline these better)|
|PreviewImageUrl|string|A low resolution rendering of the template|
|FullImageUrl|string|A full resolution rendering of the template|

### Template
`TRMS\Carousel\Models\Template`

A template is the starting point for a standard Bulletin and is comprised of a background image and a series of content Blocks.
#### Methods
|Method|Parameters|Returns|Description|
|------|----------|-------|-----------|
|setBackground|Media Object|self - chainable|Sets the background Media to be used in this model|
|getBackground|none|Media Object|Gets the related background Media model|
|addBlock|Block Object|self - chainable|Add a Block relationship to the model|
|removeBlock|Block Object|self - chainable|Remove a Block relationship from the model|
|setUser|User Object|self - chainable|Sets the User to be used in this model|
|getUser|none|User Object|Gets the related User model|
|setZone|Zone Object|self - chainable|Sets the Zone to be used in this model|
|getZone|none|Zone Object|Gets the related Zone model|
#### Properties
|Property|type|Description|
|--------|----|-----------|
|id|string|This is set by the server and not editable.|
|Name|string|The name of the template|
|Tags|array |An Array of Tag Objects|
|IsPublic|boolean|Is this template viewable by all users in the Carousel UI|
|Blocks|array|An array of Block objects|
|PreviewImageUrl|string|A low resolution rendering of the template|
|FullImageUrl|string|A full resolution rendering of the template|

### BulletinBlock
`TRMS\Carousel\Models\BulletinBlock`

A BulletinBlock is an area of content within a `Bulletin` or a `Template`.  Blocks can be `Text`, `Picture`, `Video`, or `WebPicture`.  Text blocks are just that, blocks containing text. Picture and Video blocks will take a Media Object. WebPicture blocks take the URL of an image. There are many properties on a block some of which apply to only one of the four `BlockType`s.  Many have several properties that are used to make an effect, like a drop shadow or a text glow.
#### Methods
|Method|Parameters|Returns|Description|
|------|----------|-------|-----------|
|setMedia|Media Object|self - chainable|Sets the Media to be used in this model and sets the `blockType` to the corresponding Media type.|
|getMedia|none|Media Object|Gets the related Media model.|
#### Properties
|Property|type|Description|
|--------|----|-----------|
BlockType|enumerable|Indicates the type of the block: `Rectangle`, `Ellipse`, `Text`, `Picture`, `WebPicture`, `Video`|
Name|string|The name of the block|
|**Size and Position**|
X|int|The x coordinate of the upper left corner of the block.|
Y|int|The y coordinate of the upper left corner of the block.|
Width|int|The width in pixels of the block.|
Height|int|The height in pixels of the block.|
RotateDegrees:|int|The rotation of the block in degrees|
|**Text Basic**|
Text|string|The text to be displayed in a text block|
AutoSizeText|boolean|If the block should auto size the text to fill the available block.  If false the `TextSize` will be used|
TextSize|int|The font size in points|
|**Text Style**|
TextFont|string|The font name of an installed font. (this is a relationship, getting the installed fonts is not currently supported in this package)|
TextBold|boolean|Bold styling|
TextItalic|boolean|Italic styling|
TextStrikeout|boolean|Strikeout styling|
TextUnderline|boolean|Underline styling|
|**Text Color**|
TextColor|css color value|The text color|
TextColorOpacity|float 0-1|The opacity of the text|
|**Text Alignment**|
TextHorizAlignment|enumerable|The horizontal alignment of the text: `Near`,`Far`,`Center`|
TextVertAlignment|enumerable|The horizontal alignment of the text: `Near`,`Far`,`Center`|
TextRightToLeft|boolean|Draw the text right to left|
TextWrap|boolean|Should the text line wrap|
|**Text Gradient Fill**|
TextGradient|boolean|Enable text gradient|
TextGradientColor|css color value|The color of the gradient|
TextGradientMode|enumerable|The direction of the gradient: `Horizontal`,`Vertical`,`ForwardDiagonal`,`BackwardDiagonal`|
TextGradientOpacity|float 0-1|The opacity of the gradient|
|**Text Stroke**|
TextOutline|boolean|Enable text stroke|
TextOutlineColor|css color value|The color of the stroke|
TextOutlineOpacity|float 0-1|The opacity of the stroke|
|**Text Drop Shadow**|
TextShadow|boolean|Enable text shadow|
TextShadowColor|css color value|The color of the shadow|
TextShadowDepth|int|Value in pixels of the shadow depth|
TextShadowOpacity|float 0-1|The opacity of the shadow|
|**Text Glow**|
TextGlow|boolean|Enable text glow|
TextGlowColor|css color value|The color of the text glow|
|**Block Color Fill**|
RectColor|css color value|The background fill of the block|
RectColorOpacity|float 0-1|The opacity of the fill|
|**Block Gradient**|
RectGradient||boolean|Enable block gradient|
RectGradientColor|css color value|The color of the gradient|
RectGradientMode|enumerable|The direction of the gradient: `Horizontal`,`Vertical`,`ForwardDiagonal`,`BackwardDiagonal`|
RectGradientOpacity|float 0-1|The opacity of the gradient|
|**Block Stroke**|
RectOutline|boolean|Enable block stroke|
RectOutlineColor|css color value|The color of the stroke|
RectOutlineWidth|int|The width in pixels of the stroke|
RectOutlineOpacity|float 0-1|The opacity of the stroke|
|**Block Drop Shadow**|
RectShadow|boolean|Enable block shadow|
RectShadowColor|css color value|The color of the shadow|
RectShadowDepth|int|Value in pixels of the shadow depth|
RectShadowOpacity|float 0-1|The opacity of the shadow|
|**Block Reflection**|
Reflection|boolean|Enable block reflection|
ReflectionOffset|int|Value in pixels of the reflection offset|
ReflectionHeight|int|Value in pixels of the reflection height|
ReflectionOpacity|float 0-1|The opacity of the reflection|
|**Picture Block**|
HorizAlignment|enumerable|The horizontal position of the image in the block: `Left`,`Center`,`Right`|
VertAlignment|enumerable|The vertical position of the image in the block: `Top`,`Center`,`Bottom`|
MaintainAspectRatio|boolean|Should the image stretch to fill the block|
|**Web Picture Block**|
ImageURL|string|URL of a remote image asset|

### Group
`TRMS\Carousel\Models\Group`

A group is a container for Bulletins that allows for easier viewing sorting and ordering.  Of important note is that every Bulletin is contained in a Group and must have a saved Group assigned before saving.
(full support of editing groups is a work in progress for this package.)
#### Methods
|Method|Parameters|Returns|Description|
|------|----------|-------|-----------|
|setZone|Zone Object|self - chainable|Sets the Zone to be used in this model|
|getZone|none|Zone Object|Gets the related Zone model|

#### Properties
|Property|type|Description|
|--------|----|-----------|
|id|string|This is set by the server and not editable.|
|Description|string|The name of the Group|
|Bulletins|array|An array of Bulletin Objects|

### Media
`TRMS\Carousel\Models\Media`

Media represents audio, video images and backgrounds to be used in Bulletins and Templates.  This content is Zone specific for Carousel UI users.  When uploading backgrounds the media type must be specified or the system will assume that it is an image.  Backgrounds should also be sized for the Zone they are intended for to avoid distorting the image.  Video content should be mp4.
#### Methods
|Method|Parameters|Returns|Description|
|------|----------|-------|-----------|
|setUser|User Object|self - chainable|Sets the User to be used in this model|
|getUser|none|User Object|Gets the related User model|
|addTag|Tag Object|self - chainable|Add a Tag relationship to the model.|
|removeTag|Tag Object|self - chainable|Remove a Tag relationship from the model.|
|setZone|Zone Object|self - chainable|Sets the Zone to be used in this model|
|getZone|none|Zone Object|Gets the related Zone model|
#### Properties
|Property|type|Description|
|--------|----|-----------|
|id|string|This is set by the server and not editable.|
|Name|string|The name of the Media|
|Type|enumerable|The type of media it is: `Background`,`Picture`,`Sound`,`Video`|
|Tags|array |An Array of Tag Objects|
|IsDeleted|boolean|Soft deletion property, soft deleted media will remain on the system until no Bulletins or Templates use it.|
|IsPublic|boolean|Is this media viewable by all users in the Carousel UI|
|PreviewImageUrl|string|A low resolution rendering of the Media.  For video and audio this is simply an icon.|
|FullUrl|string|The url of the asset|

### Zone
`TRMS\Carousel\Models\Zone`

A Zone is an area of real estate on screen where bulletins are displayed.  The screen (Channel) can be comprised of one or more Zones.
#### Methods
|Method|Parameters|Returns|Description|
|------|----------|-------|-----------|
|addTag|ZoneTag Object|self - chainable|Add a Tag relationship to the model|
|removeTag|ZoneTag Object|self - chainable|Remove a Tag relationship from the model|
#### Properties
|Property|type|Description|
|--------|----|-----------|
|id|string|This is set by the server and not editable.|
|AlertsActive|boolean (read only)|Are there active alerts in this zone.|
|DaylightSavings|boolean|Is daylight savings time respected|
|DefaultTransition|string|the id of the default transition used in this zone (future updates may make this a model relationship)|
|Description|string|The description of the Zone.|
|ExcludedWords|string|A comma separated list of words that shouldnt be allowed to be shown in the Zone.|
|ForceMonitorOn|boolean|Should the monitor be forced on during full screen alerts.|
|GraphicsHeight|integer|The height of the Zone in pixels|
|GraphicsWidth|integer|The width of the Zone in pixels|
|Pacing|float|A number from 0 to 1 that represents the relative pacing of bulletins when the system decides dwell time.|
|Tags|array|An array of ZoneTag objects|
|TimezoneID|string|The id of the timezone used by this Zone (future updates may make this a model relationship)|
|ZoneName|string|The name of the Zone|
|ZoneType|enumerable|The zone type: 'Bulletin','Crawl' or 'FullAlert'.  More information can be found in Carousel Help|

## Tags
Tags are metadata that can be added to the associated model.  They are used for searching and sorting content in Carousel.
### BulletinTag
`TRMS\Carousel\Models\BulletinTag`
### MediaTag
`TRMS\Carousel\Models\MediaTag`
### ZoneTag
`TRMS\Carousel\Models\ZoneTag`
#### Methods
#### Properties
|Property|type|Description|
|--------|----|-----------|
|id|string|This is set by the server and not editable.|
|TagName|string|The text of the tag|

## Bulletin Sorting
These objects are used for ordering the Bulletins in a Zone.
### BulletinOrder
`TRMS\Carousel\Models\BulletinOrder`

This represents the order of the Groups in a Zone.  Each BulletinOrderEntry represents a Group.  The order of the `OrderEntries` array will be the order of the Groups in the Zone.
#### Properties
|Property|type|Description|
|--------|----|-----------|
|id|string|This is set by the server and not editable.|
|OrderEntries|array|An ordered array of BulletinOrderEntry objects.  Their order represents the order of Groups in a Zone.|

### BulletinOrderEntry
`TRMS\Carousel\Models\BulletinOrderEntry`

This represents a Group and the order of its Bulletins.  The order of the `Bulletins` array will be the order of the Bulletins in the Group.
#### Properties
|Property|type|Description|
|--------|----|-----------|
|id|string|This is set by the server and not editable.|
|Bulletins|array|An ordered array of Bulletin ids.  Their order represents the order of Bulletins in the Group.|


## Exceptions
You can expect the following exceptions to be thrown if things go off the rails with the server, or if you attempt to do things that are unsupported or not allowed.

`TRMS\Carousel\Exceptions\CarouselAPIException`
`TRMS\Carousel\Exceptions\CarouselModelException`
`TRMS\Carousel\Exceptions\CarouselRequestException`