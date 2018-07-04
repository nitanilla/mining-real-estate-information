Django's Responsive Design Helper
=================================
Turn any Django URL into a responsive container to see what your site looks like
in all view ports on one page (given enough screen real estate, at least).

This builds on `Matt Kersley's`_ awesome `Responsive-Design-Helper`_ tool, but
with a Django twist.

.. _Matt Kersley's: http://mattkersley.com/
.. _Responsive-Design-Helper: https://github.com/mattkersley/Responsive-Design-Testing


Usage
-----
Install via the normal means and add ``responsive_design_helper`` to the list of
your ``INSTALLED_APPS`` and wire up the URLs.  Make sure that this line (or one
really similar if you know what you're doing) is the first argument second
argument in your ``patterns`` call:

::

    urlpatterns = patterns('',
        ('', include('responsive_design_helper.urls')),

        # Put the rest of your URLs down here
    )

With that out of the way, add ``responsive/`` to any of the URLs on your Django
site and sit back and watch the magic happen.


Contributing
------------

* Create something awesome -- make the code better, add some functionality,
  whatever (this is the hardest part).
* `Fork it`_
* Create a topic branch to house your changes
* Get all of your commits in the new topic branch
* Submit a `pull request`_

.. _pull request: http://help.github.com/pull-requests/
.. _Fork it: http://help.github.com/forking/


License
-------
Copyright 2012 Texas Tribune and Travis Swicegood

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
