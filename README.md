# Gazebo model collection
This repository contains a collection of models and world files for [Gazebo](http://gazebosim.org/). The models were designed for use with [Paparazzi](https://github.com/paparazzi/paparazzi) but can also be used for other projects.

To use the models, the `models` directory needs to be added to the `GAZEBO_MODEL_PATH` environment variable. To do so, add the following line to the end of `~/.bashrc`:
```
export GAZEBO_MODEL_PATH=<path to this repo>/models:$GAZEBO_MODEL_PATH
```
where `<path to this repo>` should be replaced by the path of this repository.

## Source files
Source files for sketchup (`*.skp`) have been included in the `src` directory. These can be exported to `.obj` or `.dae` files from SketchUp. Textures can be extracted from the model by exporting to `.dae` with the `Export Texture Maps` box checked. The exported files often need some tweaking to work correctly in Gazebo; see `doc/gazebo_export_hints.md` for more information.

