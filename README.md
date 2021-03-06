# SDLeafletDraw
ES6 + Babel port of Leaflet.draw (https://github.com/Leaflet/Leaflet.draw)

Adds support for drawing and editing vectors and markers on Leaflet maps.

Supports Leaflet 1.1.0+ branches.

## Installation and use
```
$ npm install sdleafletdraw
```

#### Importing `sdleafletdraw`
```js
import L from 'leaflet';
import 'sdleafletdraw';
// Include the css files
import 'sdleafletdraw/dist/leaflet.draw.css';
```

#### Create a new `L.Control.Draw` and add to an `L.Map`
```js
const map = new L.Map('map');
const editableLayers = new L.FeatureGroup();
map.addLayer(editableLayers);

const drawControl = new L.Control.Draw({
    draw: {
        polyline: false,
        circle: false,
        marker: false,
        rectangle: {
            color: 'red',
            fillOpacity: 0.1,
            opacity: 1,
            weight: 4,
        },
        polygon: {
            color: 'blue',
            fillOpacity: 0.1,
            opacity: 0.8,
            weight: 2.5,
        },
    },
    position: 'topleft',
    allowIntersection: false,
    edit: {
        featureGroup: editableLayers,  // A leaflet featureGroup
    }
});
map.addControl(drawControl);

map.on(L.Draw.Event.CREATED, (event) => {
    const { layerType, layer } = event;

    if (layerType === 'marker')
        layer.bindPopup('A popup!');

    editableLayers.addLayer(layer);
});
```
