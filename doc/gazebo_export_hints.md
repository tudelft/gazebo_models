# Exporting to Gazebo
Exporting to Gazebo is not straightforward, it is often necessary to fix the collada file to make the model render correctly. This is an overview of the most common fixes that were used to create the models in this repository:

##### Textures appear dark
The default ambient color is too dark, this can be fixed by explicitly setting it to white.  In the `.dae` file, replace `</diffuse>` by `</diffuse><ambient><color>1 1 1 1</color></ambient>`.

##### Emissive textures appear gray
The default ambient color is not black but dark gray. Set the emissive color to white using `<emissive><color>1 1 1 1</color></emissive>` and set the ambient color to black: `<ambient><color>0 0 0 1</color></ambient>`.

##### Transparency is ignored or causes depth sorting issues
Separately export the transparent object. Use an [OGRE material script](https://ogrecave.github.io/ogre/api/1.10/_material-_scripts.html) to set up the transparency:
```
material Cyberzoo/Poles
{
	technique
	{
		pass
		{
			alpha_rejection greater 128
			
			texture_unit
			{
				texture pole.png
			}
		}
	}
}

```
The material script needs to be included in the model's `.sdf` file:
```xml
<material>
  <script>
    <uri>model://cyberzoo/cyberzoo_poles</uri>
    <name>Cyberzoo/Poles</name>
  </script>
</material>
```
See the cyberzoo model as an example.

##### Incorrect smooth shading
Incorrect smoothing can sometimes be fixed by removing the `<input semantic="NORMAL" source="..."/>` lines from the `.dae` file.
