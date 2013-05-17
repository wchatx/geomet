GeoMet [![Build Status](https://secure.travis-ci.org/larsbutler/geomet.png?branch=master)](http://travis-ci.org/larsbutler/geomet)
======

Convert [GeoJSON](http://www.geojson.org/geojson-spec.html) to
[WKT/WKB](http://en.wikipedia.org/wiki/Well-known_text) (Well-Known
Text/Binary), and vice versa.

GeoMet is BSD-licensed and is intended to cover all common uses for dealing
with 2D, 3D, and 4D geometries (including 'Z', 'M', and 'ZM'). The following
geometry types are supported:

- Point
- LineString
- Polygon *
- MultiPoint *
- MultiLineString *
- MultiPolygon *
- GeometryCollection *

\* Implementation still in progress

The name "GeoMet" was inspired by "met", the German word for
[mead](http://en.wikipedia.org/wiki/Mead). It is also a shortened version of
the word "geometry".

### Installation ###

Clone the source code from git and run:

    $ python setup.py install
    
You can also install directly from the git repo using pip:

    $ pip install git+git://github.com/larsbutler/geomet.git

### Example usage ###

Coverting a 'Point' GeoJSON object to WKT:

    >>> from geomet import wkt
    >>> point = {'type': 'Point', 'coordinates': [116.4, 45.2, 11.1]}
    >>> wkt.dumps(point, decimals=4)
    'POINT (116.4000 45.2000 11.1000)'

Converting a 'Point' GeoJSON object to WKB:

    >>> from geomet import wkb
    >>> wkb.dumps(point)
    '\x00\x00\x00\x10\x01@]\x19\x99\x99\x99\x99\x9a@F\x99\x99\x99\x99\x99\x9a@&333333'
    >>> wkb.dumps(point, big_endian=False)
    '\x01\x01\x10\x00\x00\x9a\x99\x99\x99\x99\x19]@\x9a\x99\x99\x99\x99\x99F@333333&@'

Converting a 'LineString' GeoJSON object to WKT:

    >>> linestring = {'type':'LineString',
    ...               'coordinates': [[0.0, 0.0, 10.0], [2.0, 1.0, 20.0],
    ...                               [4.0, 2.0, 30.0], [5.0, 4.0, 40.0]]}
    >>> wkt.dumps(linestring, decimals=0)
    'LINESTRING (0 0 10, 2 1 20, 4 2 30, 5 4 40)'

Converting a 'LineString' GeoJSON object to WKB:

    >>> wkb.dumps(linestring)
    '\x00\x00\x00\x10\x02\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00@$\x00\x00\x00\x00\x00\x00@\x00\x00\x00\x00\x00\x00\x00?\xf0\x00\x00\x00\x00\x00\x00@4\x00\x00\x00\x00\x00\x00@\x10\x00\x00\x00\x00\x00\x00@\x00\x00\x00\x00\x00\x00\x00@>\x00\x00\x00\x00\x00\x00@\x14\x00\x00\x00\x00\x00\x00@\x10\x00\x00\x00\x00\x00\x00@D\x00\x00\x00\x00\x00\x00'
    >>> wkb.dumps(linestring, big_endian=False)
    '\x01\x02\x10\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00$@\x00\x00\x00\x00\x00\x00\x00@\x00\x00\x00\x00\x00\x00\xf0?\x00\x00\x00\x00\x00\x004@\x00\x00\x00\x00\x00\x00\x10@\x00\x00\x00\x00\x00\x00\x00@\x00\x00\x00\x00\x00\x00>@\x00\x00\x00\x00\x00\x00\x14@\x00\x00\x00\x00\x00\x00\x10@\x00\x00\x00\x00\x00\x00D@'
