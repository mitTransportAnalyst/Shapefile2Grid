# Shapefile2Grid
### Documentation of how to convert ESRI shapefile to Conveyal grid 

### 1 Install shp2json globally
https://github.com/substack/shp2json
```sh
$ npm install -g shp2json
```

### 2 Install geobuf globally
https://github.com/mapbox/geobuf
```sh
npm install -g geobuf
```

### 3 Install node-canvas and its dependencies 
In order to install the geobuf-to-grid in the next step, we need to install node-canvas first. 
https://github.com/Automattic/node-canvas

You can quickly install the dependencies by using the command for your OS:

OS | Command
----- | -----
OS X | `brew install pkg-config cairo pango libpng jpeg giflib`
Ubuntu | `sudo apt-get install libcairo2-dev libjpeg8-dev libpango1.0-dev libgif-dev build-essential g++`
Fedora | `sudo yum install cairo cairo-devel cairomm-devel libjpeg-turbo-devel pango pango-devel pangomm pangomm-devel giflib-devel`
Solaris | `pkgin install cairo pango pkg-config xproto renderproto kbproto xextproto`
Windows | [Instructions on our wiki](https://github.com/Automattic/node-canvas/wiki/Installation---Windows)

**El Capitan users:** If you have recently updated to El Capitan and are experiencing trouble when compiling, run the following command: `xcode-select --install`. Read more about the problem [on Stack Overflow](http://stackoverflow.com/a/32929012/148072).

And then install node-canvas
```sh
$ npm install canvas
```

### 4 Install geobuf-to-grid 
https://github.com/conveyal/geobuf-to-grid

```sh
$ npm install geobuf-to-grid
```

### 5 Convert shapefile zip archives to Geojson using shp2json
Firstly, we need zip the whole shapefile into one zip archives 
```sh
$ shp2json data.zip data.json
```

### 6 Convert Geojson to Geobuf using geobuf
```sh
$ json2geobuf data.json > data.pbf
```

### 7 Convert Geobuf to grid using geobuf-to-grid
Go to the folder you install geobuf-to-grid, and go to the subfolder named "build" 
Copy the data.pbf you get from step 6 to this "build" folder
And enter the following command
```sh
$ node geobuf-to-grid.js --png data.pbf data
```
The last parameter is the output prefix
Creates one .grid file for each numeric attribute in the geobuf. If --png is specified, creates log-scaled pngs as well (useful for debugging).

# Test environment
- Nodejs 6.9.2
- NPM 3.10.9
- MAC OS 10.12
Converting New Orleans shapefile with 28031 features and 9 fields costs 8 min.

