# Developing

## Setting up development environment

You will obviously start by [forking](https://github.com/openlayers/openlayers/fork) the OpenLayers repository.

### Install the dependencies

Go in the project directory and run the `npm install` that wil install the dependencies in the local node_modules folder.

### Creating the distribution

Since v.2 the extensions are provided as ES6 modules. 
To be used in a web page you have to create the distribution.

Use the gulp command to create a distribution of the project into the `/dist` directory:
````
gulp
````

To recreate the distribution on `js` file change, use the watch task
````
gulp watch
````


## Adding new extensions

To ensure the correct translation beetween the modules and the distribution on ol classes:
- Export one class per file as default
- Use the naming convention

### Naming convention

To ensure the correct translation beetween the modules and the distribution on ol classes, we use the follownig naming convention.

In Openlayers classes just replace the `point` by a `underscore`.
- Thus the `ol.layer.Vector` class must be imported as `ol_layer_Vector`.
- A new control `ol.control.MyControl` must be declared as `ol_control_MyControl`

The file name must reflect the name of the extension and should be placed in the src directory corresponding to its namespace.
Thus `ol_control_MyControl`must be created in the `./src/control/MyControl.js` file and can be used in a webpack as:
````javascript
import ol_control_MyControl from 'ol-ext/control/MyControl';
````

Example:
````javascript
// Import ol classes
import ol from 'ol'
import ol_control_Control from 'ol/control/control'

// Create my control
var ol_control_MyControl = function(options) {
  ol_control_Control.call(this,options);
}
ol.inherits(ol_control_MyControl, ol_control_Control);

// Export my control
export default ol_control_MyControl

````


## Building the documentation:

The documentation use [gulp-jsdoc3](https://www.npmjs.com/package/gulp-jsdoc3) to create the doc.

1. install the gulp-jsdoc3 project at the root directory:
````
npm install gulp-jsdoc3
````
2. then run the gulp command to create the doc in the [doc/doc-pages](http://viglino.github.io/ol-ext/doc/doc-pages/) directory:
````
gulp doc
````

