[![Build Status](https://secure.travis-ci.org/customink-webops/stoplight.png?branch=master)](http://travis-ci.org/customink-webops/stoplight)

Description
===========
Stoplight is a build monitoring tool that is largely based off greenscreen, but is much improved and expandable. To quickly name a few, Stoplight has:

* built-in support for Jenkins
* built-in support for Travis-CI (http://travis-ci.org)
* custom provider support
* community contributions
* full test suite
* resuable DSL

Stoplight is designed to be displayed on large television screens or monitors. It automatically resizes to fill the maximum real estate the screen can offer.

This cookbook configures a node to run one or more Stoplight applications.  The cookbook uses the [Stoplight project](https://github.com/customink/stoplight).

Requirements
============

## Cookbooks:

Opscode Cookbooks (http://community.opscode.com/cookbooks)

* git


Attributes
==========

* `default['stoplight']['install_dir']` - Location where the Stoplight application will run
* `default['stoplight']['servers']` - An array of Stoplight configuration instances
* `default['stoplight']['servers']['name']` - The name of this Stoplight
* `default['stoplight']['servers']['apache']['port']` - The port used by this Stoplight
* `default['stoplight']['servers']['apache']['server_name']` - The apache server name
* `default['stoplight']['servers']['apache']['server_admin']` - The apache server admin
* `default['stoplight']['servers']['servers']` - An array of servers (providers) that this Stoplight should watch
* `default['stoplight']['servers']['servers']['url']` - The URL for this build server
* `default['stoplight']['servers']['servers']['username']` - The login for this server (optional)
* `default['stoplight']['servers']['servers']['password']` - The password for this server (optional)
* `default['stoplight']['servers']['servers']['projects']` - Array of jobs to poll for.  Leave empty to watch all projects
* `default['stoplight']['servers']['servers']['ignored_projects']` - Array of projects to ignore.  Leave empty to watch all projects


License and Authors
===================

Author:: Seth Vargo <svargo@customink.com>

Copyright:: 2012, CustomInk, LLC.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
