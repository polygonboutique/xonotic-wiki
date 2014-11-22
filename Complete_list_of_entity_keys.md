Complete list of entity keys
============================

-   On all entities
    -   **`angle`:** shorthand for just setting the yaw angle
    -   **`angles`:** angles vector
    -   **`origin`:** origin vector
    -   **`targetname`:** name of the entity so it can be referenced by **`target`** keys.
-   On brush entities, classname **`func_group`** and classname **`misc_model`**:
    -   **`_castShadows`, `_cs`:** sets whether the entity casts shadows
    -   **`_celshader`:** [CelShader](CelShader) to use
    -   **`_lightmapsamplesize`, `_samplesize`:** sample size to use for surfaces of this entity
    -   **`_receiveShadows`, `_rs`:** sets whether the entity receives shadows
    -   **`_shadeangle`, `_smoothnormals`, `_sn`, `_smooth`:** largest angle between faces to allow to treat them part of the same nonplanar surface
    -   **`lightmapscale`, `_lightmapscale`, `_ls`:** scaling factor for the lightmap resolution
-   On brush entities and on classname **`func_group`**:
    -   **`_indexmap`, `alphamap`:** file name of index map image for terrain blending
    -   **`_layers`, `layers`:** number of layers of the index map image (encoded as brightness levels)
    -   **`_offsets`, `offsets`:** space separated list of z offsets
    -   **`_shader`, `shader`:** shader name prefix of the index map (when this is set to `X`, the shader names that are generated will be like `textures/X_42` and `textures/X_23to42`
-   On brush entities
    -   **`_clone`, `_ins`, `_instance`:** **`_clonename`** field value of a brush entity to clone brushes from (can be used to use the same brush model multiple times)
    -   **`_clonename`:** see **`_clone`**
    -   **`_patchMeta`, `patchMeta`:** generate a triangle soup from patches in this entity
    -   **`_patchQuality`:** quality multiplier for patches on this surface when **`_patchMeta`** is used
    -   **`_patchSubdivide`:** absolute quality setting for patches on this surface when **`_patchMeta`** is used
    -   **`max`:** override the `maxs` vector of this brush entity
    -   **`min`:** override the `mins` vector of this brush entity
-   On classname **`worldspawn`**
    -   **`_ambient`, `ambient`:** amount of ambient light
    -   **`_blocksize`, `blocksize`, `chopsize`:** block size for unconditional BSP subdivisions
    -   **`_farplanedist`, `fogclip`, `distancecull`:** far plane distance for vis culling — this must be the shortest distance at which nothing can be seen any more due to fog
    -   **`_floodlight`:** a quintuple of values “r g b dist intensity” to set global floodlight parameters (good defaults are 240 240 255 1024 128)
    -   **`_fog`, `fog`:** if set, the whole map is fogged using the given shader name
    -   **`_foghull`:** must be set to a sky shader when `_fog` is used
    -   **`_ignoreleaks`, `ignoreleaks`:** when set, no leak test is performed
    -   **`_keepLights`:** if set, **`light`** entities are not stripped from the `BSP` file when compiling
    -   **`_mingridlight`:** amount of minimum grid light
    -   **`_minlight`:** amount of minimum light
    -   **`_minvertexlight`:** amount of minimum vertex light
    -   **`_noshadersun`:** if set, sun light from shaders is suppressed
    -   **`_q3map_cmdline`:** written by q3map2; contains the command line the map was compiled with
    -   **`_q3map_version`:** written by q3map2; contains the version of q3map2 the map was compiled with
    -   **`_style42alphagen`:** |alphaGen|-like shader definition string for light style 442 (works the same way for all style numbers)
    -   **`_style42rgbgen`:** |rgbGen|-like shader definition string for light style 42 (works the same way for all style numbers)
    -   **`gridsize`:** resolution of the light grid
-   On classname **`light`** and classname **`lightJunior`**
    -   Note: **`lightJunior`** entities only affect the light grid.
    -   **`_anglescale`:** scales angle attenuation
    -   **`_color`:** color of the light
    -   **`_deviance`, `_deviation`, `_jitter`:** position deviance of the samples of a regular light (distributes the light samples in a cube of side length 2\*\_deviance around the origin), or angle deviance of the sun light samples in radians
    -   **`_filterradius`, `_filteradius`, `_filter`:** filter radius for this light, similar to -light -filter
    -   **`_samples`:** number of samples to use to get soft shadows from a light
    -   **`_sun`:** if 1, this light is an infinite sun light
    -   **`fade`:** Fade factor of light attenuation of linear lights. Linear lights completely vanish at distance **`light`**/(**`fade`** \* 8000), so if you want the light to vanish at distance X, specify **`light`**/(8000\*X) here.
    -   **`light`:** intensity factor (default: 300)
    -   **`radius`:** radius of a spotlight at the target point (default: 64)
    -   **`scale`:** intensity multiplier
    -   **`spawnflags`:** 1 = linear attenuation (inverted in `-wolf` lighting mode)
    -   **`spawnflags`:** 2 = no angle attenuation (inverted in `-wolf` lighting mode)
    -   **`spawnflags`:** 32 = the light color is not normalized
    -   **`spawnflags`:** 64 = force distance attenuation (why did vortex add this, this is always set...?)
    -   **`target`:** target of a spotlight
    -   **`targetname`:** when set, the light can be toggled in game by some engine provided way
-   On classname **`light`**
    -   **`_flare`:** when set, this light is a flare without a specified shader
    -   **`_flareshader`:** shader for a flare surface generated by this light
    -   **`_style`, `style`:** light style number
    -   **`spawnflags`:** 16 = light does not affect the grid
-   On classname **`advertisement`** (QuakeLive only)
    -   Brushes/Patches: must be a single rectangular patch surface where the ad will be placed
    -   **`cellId`:** identifier of the ad, must be used only once (??)
-   On classname **`_decal`**
    -   Brushes/Patches: must be a single rectangular patch surface
    -   **`target`:** positional target to set the projection direction of the decal
-   On classname **`misc_model`**
    -   **`_castShadows`, `_cs`:** sets whether the entity casts shadows
    -   **`_frame2`:** frame of second model to load
    -   **`_frame`:** frame of model to load
    -   **`_receiveShadows`, `_rs`:** sets whether the entity receives shadows
    -   **`_remapXXX`:** `XXX` can be any string to allow multiple keys for this; contains a string of the form `from;to`, and any shader `from` in the model will be replaced by `to`; the special value `*` in `from` matches all shader names
    -   **`model2`:** path name of second model to load
    -   **`model`:** path name of model to load
    -   **`modelscale`:** scaling factor for the model to include
    -   **`modelscale_vec`:** non-uniform scaling vector for the model to include
    -   **`spawnflags`:** 1 = in SoF2, append a `_RMG_BSP` suffix to shader names instead of `_BSP`
    -   **`spawnflags`:** 2 = generate clipping brushes from the model
    -   **`spawnflags`:** 4 = force this model through meta surface merging
    -   **`spawnflags`:** 8 = when generating clipping planes, perform extrusion using the original normals from the model instead of per-triangle best axial normals
    -   **`spawnflags`:** 16 = when generating clipping planes, perform extrusion using only up or down pointing normals (ideal for terrain)
    -   **`spawnflags`:** 24 = when generating clipping planes, perform extrusion by distance zero (needs engine changes to support zero-volume clipping brushes)
    -   **`spawnflags`:** 32 = turn vertex color from the model into alpha (for terrain blending)
    -   **`spawnflags`:** 64 = do not let picomodel do surface normal smoothing
-   On classname **`_skybox`**
    -   To be placed inside a small otherwise hidden room; surfaces in it are scaled up, and visible through skybox surfaces
    -   **`_scale`:** scaling factor or vector for the portal sky (default: 64)
