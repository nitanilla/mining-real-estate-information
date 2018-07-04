Django Homegate
============

django-homegate (https://github.com/arteria/django-homegate) provides IDX3.01 API support for your Django project by closing the gap between python-homegate (https://github.com/arteria/python-homegate) and your real estate Django app.


Installation
------------

To get the latest stable release from PyPi

.. code-block:: bash

    $ TODO
	
To get the latest commit from GitHub

.. code-block:: bash

    $ pip install -e git+git://github.com/arteria/django-homegate.git#egg=django_homegate 
	
Add ``django_homegate`` to your ``INSTALLED_APPS``

.. code-block:: python

    INSTALLED_APPS = (
        ...,
        'django_homegate',
    )

 
 


Usage
-----

django-homegate is a helper app providing a management command to push the new records to Homegate using the API implementation of python-homegate (https://github.com/arteria/python-homegate). If you install from  PyPi, this package will be installed as dependency.

To connect you real estate model, register your model in the settings and implement a model manager method that returns all records (real estate objects) to push to Homegate. In addition, a ``get_idx_record()`` and ``published_idx_record()`` method must be implemented on your real estate model to get access to the data to push to Homegate and to update the status of the record. There is an example provided in ``django_homegate/models.py``. 

To register the model do not forget to set the app label in your real estate model, eg. '<real-estate>', and in your settings.py add ``HOMEGATE_REAL_ESTATE_MODEL = '<your-app>.models.<real-estate-class>'``.


The manager method name is ``ready_to_push()``, so
	
.. code-block:: python

	>>> objs = RealEstate.objects.ready_to_push()
	
will return a QuerySet containing all real estate objects to publish to Homegate. There is an example provided in ``django_homegate/models.py`` as well. 


In ``settings.py`` add ``HOMEGATE_AGENCY_ID = '<your-agency-id>'``,  ``HOMEGATE_HOST = '<homegate-host>'``, ``HOMEGATE_USERNAME = '<your-username>'`` and  ``HOMEGATE_PASSWORD = '<your-password>'``.


For more info about model managers and app labeling see:

http://www.djangobook.com/en/2.0/chapter10.html 

https://docs.djangoproject.com/en/dev/ref/models/options/#django.db.models.Options.app_label


Contribute
----------

If you want to contribute to this project, please perform the following steps

.. code-block:: bash

    # Fork this repository
    # Clone your fork
    $ mkvirtualenv -p python2.7 django-homegate
    $ python setup.py install
    $ pip install -r dev_requirements.txt

    $ git co -b feature_branch master
    # Implement your feature and tests
    $ git add . && git commit
    $ git push -u origin feature_branch
    # Send us a pull request for your feature branch


.. image:: https://d2weczhvl823v0.cloudfront.net/philippeowagner/django-homegate/trend.png
   :alt: Bitdeli badge
   :target: https://bitdeli.com/free

