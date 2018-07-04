# ImageListing


Image finder goes to a given web page and gets a list of largest images(by screen real estate each image taken; width x height) on that page

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'image_listing'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install image_listing

## Usage


 ```ruby
  require 'image_listing'
  @image_list   = ImageListing::ImageListing.new

  info_array = @image_list.get_the_sizes_of_images_limited("http://iamfree.com", 5)

  #to get an array of image urls
  info_array.transpose[2]
 ```
  [300, 429, "http://graphics.iamfree.com/artworks/491/medium/a-house-in-the-wild-side.jpg?1386595326", 128700]

  width, height, image url, width x height(screen real estate taken in pixcels)

  get only image list  


  To get all images from page

  ```ruby
  #images with sizes
  images_array = @image_list.get_the_sizes_of_images

  #then list of images
  images_array.transpose[2]
 ```

## Contributing

1. Fork it ( https://github.com/iamfree-com/image_listing/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
