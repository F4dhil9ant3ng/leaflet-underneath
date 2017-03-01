# Leaflet Underneath

[![Greenkeeper badge](https://badges.greenkeeper.io/perliedman/leaflet-underneath.svg)](https://greenkeeper.io/)
[![NPM version](https://img.shields.io/npm/v/leaflet-underneath.svg)](https://www.npmjs.com/package/leaflet-underneath) !

[Check out the demo](http://www.liedman.net/leaflet-underneath/)

With a normal tile layer, the user can't interact to find out more about a location, since it is a static image. With this plugin, you can find out what features are underneath the current mouse position, for example when the user clicks the map.

This is done using [Mapbox Vector Tiles](https://www.mapbox.com/developers/vector-tiles/), that are queried for features in a way that is both fast and reasonably bandwidth efficient.

## Using

[Download](https://github.com/perliedman/leaflet-underneath/releases) the code. Include the pre-built Leaflet Underneath script in your project:

```html
    <script src="leaflet-underneath/dist/leaflet-underneath.js"></script>
```

or, even better, use Browserify or similar and install from npm:

```
npm install --save leaflet-underneath
```

```javascript
var L = require('leaflet');
require('leaflet-underneath');

// Leaflet Underneath will be available as L.tileLayer.underneath
```

For a complete example on how to use Leaflet Underneath, see basic [Leaflet Underneath example](https://github.com/perliedman/leaflet-underneath/blob/master/example/index.js).

## API

### L.TileLayer.Underneath

Leaflet Underneath uses a tilelayer that can be queried for features from a location. The layer extends
[L.TileLayer](http://leafletjs.com/reference.html#tilelayer).

#### Creation

Factory              | Description
---------------------|-----------------------------
`L.tileLayer.underneath(<String> tileUrl, <`[`UnderneathOptions`](#underneathoptions)`> options?) | Instantiates a new Leaflet Underneath layer

#### Options

In addition to Leaflet's built-in [TileLayer options](http://leafletjs.com/reference.html#tilelayer-options), Leaflet Underneath has these options:

Option                 | Type          | Default              | Description
-----------------------|---------------|----------------------|----------------------------
`layers`               | `String[]`    | `[]`                 | Names of layers to include in search
`defaultRadius`        | `Number`      | `20`                 | Default number of pixels search radius
`featureId`            | `Function`    |                      | Function that returns a unique feature id; used to filter out duplicates. Default returns a features `osm_id`property
`lazy`                 | `Boolean`     | `true`               | If lazy, only tiles that are queried will be loaded. Otherwise, all tiles will be loaded, like a normal tile layer.
`zoomIn`               | `Number`      | `0`                  | Zoom in relative to the map's current zoom level when making a query; used to get more or less detailed results than current zoom would give
`joinFeatures`         | `Boolean`     | `false`              | For features with same id, should geometries be joined (`true`), or should they be ignored (`false`)

#### Methods

Method                          | Returns                   | Description
--------------------------------|---------------------------|--------------------------
`query(<`[`L.LatLng`](http://leafletjs.com/reference.html#latlng)`> latLng, <Function> callback, <Object> context, <`[`QueryOptions`](#queryoptions)> options?)` | `this` | Asynchronously queries for features near `latLng`; `callback` will be called with features within `radius` pixels of the coordinate

#### QueryOptions

Option                 | Type          | Default              | Description
-----------------------|---------------|----------------------|----------------------------
`radius`               | `Number`      | Take from layer options | Number of pixels search radius
`onlyInside`           | `Boolean`     | `false`              | Only return features (polygons) that the queried location is inside
