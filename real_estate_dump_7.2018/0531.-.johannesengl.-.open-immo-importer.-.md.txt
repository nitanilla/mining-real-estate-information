## Open Immo Importer

Synchronize real estate properties in the open immo xml format via ftp and create property records.

### OpenImmo Module

ftp_importer.rb
- download real estate xml, jpg and pdf files from ftp sever to local directory
- extract zip files
- read in xml files

property_item.rb
- interface to create property records and associations from xml data

property_loader.rb
- check if new files available for import from ftp
- sync new estate properties

Tests
----
The tests accessing real estate data for a ftp server are mocked using files from the folder spec/fixtures/estate_export.
The tests accessing external Services are mocked with the 'vcr' gem to be faster and executable without internet connection.

To execute the test suite run
```sh
rspec
```

License
----
MIT

