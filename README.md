# Gazebo model collection
This repository contains a collection of models and world files for [Gazebo](http://gazebosim.org/). The models were designed for use with [Paparazzi](https://github.com/paparazzi/paparazzi) but can also be used for other projects.

To use the models, the `models` directory needs to be added to the `GAZEBO_MODEL_PATH` environment variable. To do so, add the following line to the end of `~/.bashrc`:
```
export GAZEBO_MODEL_PATH=<path to this repo>/models:$GAZEBO_MODEL_PATH
```
where `<path to this repo>` should be replaced by the path of this repository.

The models and worlds work in Gazebo Classic and in the new Gazebo (gz-sim, Harmonic and later). For the new Gazebo, use `GZ_SIM_RESOURCE_PATH` instead of `GAZEBO_MODEL_PATH`; the worlds include `model://ground_plane` from the Gazebo Classic model database, which the new Gazebo does not have (Paparazzi provides one).

Rules that keep a model or world working in both:
- Collisions: use simple shapes (box, cylinder); a large mesh collision crashes or hangs the new Gazebo physics.
- Materials: Ogre material scripts (`<script>`) only work in Gazebo Classic; add a `<pbr>` `<albedo_map>` with the texture for the new Gazebo, or use `<ambient>`/`<diffuse>` colours.
- Meshes: large COLLADA files load very slowly in the new Gazebo; use OBJ. A mesh without texture coordinates cannot show a texture: give it a colour.
- Worlds: the new Gazebo ignores the `<state>` block that Gazebo Classic writes when a world is saved: put the poses in the models, and `<include>` the models of this repository instead of saving copies of them in the world.

## Source files
Source files for sketchup (`*.skp`) have been included in the `src` directory. These can be exported to `.obj` or `.dae` files from SketchUp. Textures can be extracted from the model by exporting to `.dae` with the `Export Texture Maps` box checked. The exported files often need some tweaking to work correctly in Gazebo; see `doc/gazebo_export_hints.md` for more information.

