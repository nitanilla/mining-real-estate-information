# REAL ESTATE WITH PURPOSE

## Local

* ```git clone``` [https://github.com/the-difference-engine/real-estate-with-purpose.git]

* ```bundle install```

* ```rake db:create```

* ```rake db:migrate```

* To start server: ```rails server```

* To run tests: ```rspec spec```

* Rails version 5.0

### Dependencies

This app uses the Paperclip gem and requires ImageMagick. To check that you have it on your computer, open terminal, run ```which convert``` (one of the ImageMagick utilities). This will give you the path where that utility is installed. For example, it might return ```/usr/local/bin/convert```

To install with Homebrew:

```brew install imagemagick```

If you are on Ubuntu (or any Debian base Linux distribution), you'll want to run the following with apt-get:

```sudo apt-get install imagemagick -y```

### Environment Variables

* ```touch .env```

#### SimplyRETS API

* USERNAME

* PASSWORD

#### Google Maps API

* GOOGLE
