Real Estate Sample App
======================

A sample real estate app showing how to:
  - use Maven build system with multiple modules
  - use Robolectric, Robotium and Calabash for testing
  - use Navigation Drawer and ActionBarCompat
  - support multiple screen sizes
  - use Event Bus for decoupling fragments and activities
  - use Picasso for image loading and Retrofit for HTTP requests
  - use maven to upload apks to [TestFairy](https://app.testfairy.com/) and run [monkey](http://developer.android.com/tools/help/monkey.html)

Calabash
=====
  - In this project I used a custom calabash-android gem from this [pull request](https://github.com/calabash/calabash-android/pull/329)
  - To install Calabash:
    - install Apache Ant
    - follow the prerequisite steps from [calabash-android](https://github.com/calabash/calabash-android/blob/master/documentation/installation.md)
    - install bundler gem ```gem install bundler```
    - checkout calabash-android from pull request:
```git clone https://github.com/AlexeyDsov/calabash-android.git -b callActivityMethod```
    - follow the steps from [here](https://github.com/calabash/calabash-android/wiki/Building-calabash-android) without git clone
    - when the gem is built go to ```pkg``` folder and execute:
```gem install [name of the gem].gem```
  - Usage is described [here](https://github.com/calabash/calabash-android) and a list of predefined steps is [here](https://github.com/calabash/calabash-android/blob/master/ruby-gem/lib/calabash-android/canned_steps.md)

Known issues on IntelliJ
=====
**Problem**: When running a Robolectric Test a "Stub!" exceptions occurs.<br>
**Solution**: Open Module Settings -> Dependencies and move Android framework to the bottom

**Problem**: When running a Robolectric Test *AndroidManifest.xml* is not found.<br>
**Solution**: A correct module needs to be selected. Edit run configuration and select *real-estate* instead of *real-estate-parent* for *Use classpath of module*

**Problem**: No Android SDK selected.<br>
**Solution**: Select *real-estate-all*, right-click and select Open Module Settings. Select your Java and Android SDK locations.

**Problem**: IntelliJ cannot find ActivityName_ classes<br>
**Solution**: Add generated source code to source root [description](http://hintdesk.com/android-introduction-to-androidannotations-maven-in-intellij-idea/)

**Problem**: When running SqlGenerator a FileNotFoundException is thrown<br>
**Solution**: Make sure that in your Run Configuration you have set *sql-generator* as your Working Directory

