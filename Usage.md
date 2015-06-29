# Creating and saving `GeoModel`-derived entities #
To use the `GeoModel` class, simply declare a new model class inheriting from the `geo.GeoModel` class like so:

```
from geo.geomodel import GeoModel

class MyEntity(GeoModel):
  foo = db.StringProperty()
  bar = db.IntegerProperty()
```

Currently, only single-point entities are supported. Entities of the new `MyEntity` kind will have a `location` property of type `db.GeoPt`, which can be set as needed. Before `put()`'ing entities to the datastore, make sure to call `update_location` to synchronize the entity's underlying geocell indexing properties:

```
some_entity = MyEntity(location=db.GeoPt(37, -122),
                       foo='Hello',
                       bar=5)
...
some_entity.location = db.GeoPt(38, -122)
some_entity.update_location()
some_entity.put()
```

# Querying your entities #

There are currently two types of basic geospatial queries supported by the GeoModel library:

  * bounding box queries
  * proximity (nearest-n) queries

To perform a bounding box query, use the `bounding_box_fetch` class method like so:

```
results = MyEntity.bounding_box_fetch(
              MyEntity.all().filter('bar >', 5),  # Rich query!
              geotypes.Box(39, -121, 37, -123),
              max_results=10)
```

Be careful not to request too many results or else you'll get a datastore or request timeout!

To perform a proximity query, use the `proximity_fetch` class method like so:

```
resuts = MyEntity.proximity_fetch(
             MyEntity.all().filter('bar <', 10),  # Rich query!
             geotypes.Point(39, -121),  # Or db.GeoPt
             max_results=10,
             max_distance=80467)  # Within 50 miles.
```

Note that for rich queries on multiple properties you'll need to set up the proper indexes in your `index.yaml` file. Testing your app on the development server should populate that file with the required indexes. Also, `GeoModel` currently requires many internal properties on each entity (one for each geocell resolution), which can lead to messy looking `index.yaml` files. That's something that will hopefully change in future versions.