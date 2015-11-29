Explosion shader effect
for integration into Unreal Engine 4 projects

Created by Roman Komary 2014-2015

This is "Explosion effect" https://www.shadertoy.com/view/Xd3GWn

Based on huwb's Anatomy of an explosion https://www.shadertoy.com/view/Xss3DS
and on iq's Hell https://www.shadertoy.com/view/MdfGRX

For license, see included Expl/license.txt.


This implements a raymarching shader to approximate emulation of an explosion effect.

Notice, the integration as Unreal assets is performed using custom nodes in Unreal materials.
To make it work with custom nodes, quite several (somewhat dirty) hacks have been introduced.

Therefore the shaders in this package should not be considered as appropriate for production purposes.
But this is just a recommendation.

The package has been created using Unreal Engine 4.9. A test with currently newest version 4.10 still works the
same.

Anyway, since the shader bases on arts from shadertoy.com which run under a non-commercial creative commons license,
I am forced to put this explosion shader (and iSphere shader) also under the same license (see Expl/license.txt).
See http://creativecommons.org/compatiblelicenses for CC BY-NC-SA 3.0.

This license applies solely to the shader source codes plus the material assets that include the custom nodes with shader source codes.


The shaders can be found inside the Content/Expl folder. Material "ExplosionShader" contains the shaders in custom nodes. For easy of reading and editing, the shader codes themselves are available in several files named *.usf.txt

The assests building on top of the materials (so material instances and particle systems) in this folder are just for testing.


For some documentation regarding the problems and hacks used in the shader, have a look at the other text files in this package.
Also have a look at comment nodes (and description texts in comment nodes) of the materials in this package.

Especially notes_shader_expressions.txt describes my tries to setup custom expressions to work for the explosion shader needs.


Usage:

Create a material instance from the shader material, put it into a particle system that is "PSA Facing Camera Position" and "PSORTMODE Distance to View".

The particle emitter also has to define 3 parameters for the material which acts as seed values. We want them random per particle.
So add a Dynamic Parameter (which has 4 parameters). And for the first 3 values each, set the Distribution Float Uniform in the range from -1000 to 1000 and don't forget to set "Spawn Time Only".

Usually you will want to set particle system's "Use Local Space" off (in Required).
But the shader can take object orientation and scale into account if "Use Local Space" is set to on. It will then take the orientation of the whole particle system into account which is useful for explosion effects that have a directional look (that is when ball_spread is less than 1.0 being close to 0.0) in a different direction than the world's up vector, so e.g. on a wall where the explosion should extrude towards the side.

Just play with the parameters in the material instance to your needs.

The material exposes quite many parameters, most of them being not independent to each other, that is one parameter change might require adjustments of some others. Best approach is trial and error.
