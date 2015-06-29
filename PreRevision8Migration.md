# Introduction #

If you started using GeoModel before [Revision 8](http://code.google.com/p/geomodel/source/detail?r=8), then you may need to perform a migration of your entities to the new version, which is much cleaner in with respect to `index.yaml` definition/maintenance, among other things.

As of [Revision 8](https://code.google.com/p/geomodel/source/detail?r=8), GeoModel entities no longer have multiple `StringProperty`s for storing geocells (i.e. `location_geocell_1`, `location_geocell_2`, etc.). Instead, they now have a single `StringListProperty` named `location_geocells`.

The details of why this decision was made can be found in [Issue 4](https://code.google.com/p/geomodel/issues/detail?id=4).

# Migration Procedure #

The basic idea is that you simply need to update your GeoModel library to the latest version and call `entity.update_location()` for each entity in the datastore. It may also help to set the previous `location_geocell_n` properties to `None`.

There is a script in the [PubSchools demo source directory](http://code.google.com/p/geomodel/source/browse/trunk/demos/pubschools) named [location\_geocell\_migration.py](http://code.google.com/p/geomodel/source/browse/trunk/demos/pubschools/scripts/batch/location_geocell_migration.py), which uses the [Mapper framework](http://code.google.com/appengine/articles/remote_api.html) to bulk edit entities remotely. All you need to do is download that script and its dependencies ([remote\_client.py](http://code.google.com/p/geomodel/source/browse/trunk/demos/pubschools/scripts/batch/remote_client.py) and [mapper.py](http://code.google.com/p/geomodel/source/browse/trunk/demos/pubschools/scripts/batch/mapper.py)), tweak it to adapt to your own application's models, and run it.

Once it's complete, you may need to reconfigure your `index.yaml` file and probably also run `appcfg.py vacuum_indexes` to get rid of the old indexes.

# Help #

If you run into any problems with this migration path, feel free to post in the comments.