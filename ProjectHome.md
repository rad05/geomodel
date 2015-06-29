This project aims to provide a generalized solution for performing basic indexing and querying of geospatial data in [Google App Engine](http://code.google.com/appengine).

At the core, this solution utilizes [geohash](http://www.google.com/url?sa=U&start=1&q=http://en.wikipedia.org/wiki/Geohash)-like objects called [geocells](http://code.google.com/p/geomodel/source/browse/trunk/geo/geocell.py).

Currently, only single-point entities and two types of basic geospatial queries on those entities are supported:

  * bounding box queries
  * proximity (nearest-n) queries

For another approach to geo queries in Google App Engine, see the [mutiny project](http://code.google.com/p/mutiny) and its [associated article](http://code.google.com/appengine/articles/geosearch.html), or the geohash-based [geodatastore](http://code.google.com/p/geodatastore) project.

## PyPi ##

Thanks to the awesome work of Tobias Rodäbel, this library is now available at http://pypi.python.org/pypi/geomodel!

## Java ##

Thanks to the awesome work of Alexandre Gellibert, this library is now available for [Google App Engine for Java](http://code.google.com/appengine/docs/java/overview.html) at http://code.google.com/p/javageomodel!

## PubSchools Demo Application ##

To get an idea of how to use GeoModel in a real world application, check out the [PubSchools demo](http://geomodel-demo.appspot.com) and its [source code](http://code.google.com/p/geomodel/source/browse/trunk/demos/pubschools). Below is a screenshot of a sample query for public schools in San Francisco, CA:

[![](http://geomodel.googlecode.com/svn/trunk/demos/pubschools/thumb.png)](http://geomodel-demo.appspot.com)