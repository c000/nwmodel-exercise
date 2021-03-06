# nwmodel-exercise

[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

Exercise of Network Topology Model ([RFC 8345 \- A YANG Data Model for Network Topologies](https://datatracker.ietf.org/doc/rfc8345/))

See also [the topology data checker](https://github.com/corestate55/nwmodel-checker).

## Directory

* `src`: Source code files of visualizer.
  * Codes are packed by `webpack` and stored in `dist` as `main.js`.
* `dist`: Distributed files. (`devServer`'s document-root)
* `dist/model`: Topology data files (json)

This visualizer depends on [D3.js v4](https://d3js.org/), [Webpack](https://webpack.js.org/), [Node.js](https://nodejs.org/ja/) and [NPM](https://www.npmjs.com/).

## Demo

The visualizer works on Heroku.

* https://nwmodel-vis.herokuapp.com/

## Installation

### Install packages

Install Node.js and NPM at first in your system.

Install packages used by this visualizer (according to `package.json`).
```
npm install
```

### Run web server
Run `webpack-dev-server`.
```
npm run start
```
Then, it opens dist/index.html with browser.

### Build

Run `webpack`
```
npm run build
```

### Lint

Run `eslint`.
```
npm run lint
```

## Structure

```
 augmented topology data model        topology data structure       graph object structure        visualizer
 (RFC8346,                            (RFC8345)
 draft-ietf-i2rs-yang-l2-network-topology)
                                        +-----------+                   +-----------+            +-----------+
              +-------------------------| networks  |-------------------|  graphs   |<|----------|visualizer |
              |                         +-----+-----+                   +-----+-----+ whole      +-----+-----+
        +-----+-----+                         |                               |       layerrs          |
        |   L2/L3   |                   +-----+-----+                   +-----+-----+            +-----+-----+
        |  network  |-----------------|>| network   |                   |  graph    | single     |operational|
        +-----+-----+                   +-----+-----+                   +-----+-----+ layer      |visualizer | event
              |                               |                               |                  +-----+-----+ handling
      +-------+-------+               +-------+-------+               +-------+-------+                |
      |               |               |               |               |               |                V
      |         +-----+-----+         |               |               |    node +-----+-----+    +-----+-----+
      |         |   L2/L3   |         |         +-----+-----+         |  object |  graph    |    |simulated  |
      |         |   node    |---------(-------|>|   node    | . . . . ( . . . . |   node    |    |visualizer | force
      |         +-----+-----+         |         +-----+-----+         |         +-----------+    +-----+-----+ simulation
+-----+-----+         |               |               |   tp-tp +-----+-----+         : tp             |
|   L2/L3   |         |         +-----+-----+         |    link |  graph    |         : object         V
|   link    |---------(-------|>|   link    | . . . . (. . . . .|   link    |         :          +-----+-----+
+-----------+         |         +-----------+         |         +-----------+         :          |single     |
                      |                               |               : tp-node       :          |visualizer | static
                +-----+-----+                         |               : link          :          +-----------+ graph
                |   L2/L3   |                   +-----+-----+         :               :                        object
                | term pts  |-----------------|>| term pts  | . . . . : . . . . . . . :
                +-----------+                   +-----------+
```

See more detail, [class diagram in fig directory](./fig/).
