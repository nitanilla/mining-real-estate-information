GeoModel uses geohash-like objects called 'geocells' to provide a generalized
solution for indexing and querying geospatial data in App Engine.  GeoModel is
optimized for the basic real estate finder/store locator use case, but can be
adapted for use with large datasets.

Using GeoModel, developers can instantly geo-contextualize datastore models by
simply inherting from the GeoModel class. Currently, entities can be associated
with a single geographic point and subsequently indexed and filtered by either
conformance to a bounding box or by proximity (nearest-n) to a search center
point.
