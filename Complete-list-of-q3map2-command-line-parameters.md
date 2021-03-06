Complete list of q3map2 command line parameters
========================================

Common options
--------------

-   **`-connect` address:** Talk to a NetRadiant instance using a specific XML based protocol
-   **`-force`:** Allow reading some broken/unsupported BSP files e.g. when decompiling, may also crash
-   **`-fs_basepath` path:** Sets the given path as main directory of the game (can be used more than once to look in multiple paths)
-   **`-fs_game` gamename:** Sets a different game directory name (default for Q3A: baseq3)
-   **`-fs_homebase` dir:** Specifies where the user home directory name is on Linux (default for Q3A: .q3a)
-   **`-game` gamename:** Load settings for the given game (default: quake3)
-   **`-subdivisions` F:** multiplier for patch subdivisions quality
-   **`-threads` N:** number of threads to use
-   **`-v`:** Verbose mode

BSP stage
---------

-   **`-bsp` ... filename.map:** Switch that enters this stage
-   **`-altsplit`:** Alternate BSP tree splitting weights (should give more fps)
-   **`-celshader` shadername:** Sets a global cel shader name
-   **`-custinfoparms`:** Read scripts/custinfoparms.txt
-   **`-debuginset`:** Push all triangle vertexes towards the triangle center
-   **`-debugportals`:** Make BSP portals visible in the map
-   **`-debugsurfaces`:** Color the vertexes according to the index of the surface
-   **`-deep`:** Use detail brushes in the BSP tree, but at lowest priority (should give more fps)
-   **`-de` F:** Distance epsilon for plane snapping etc.
-   **`-fakemap`:** Write fakemap.map containing all world brushes
-   **`-flares`:** Turn on support for flares (TEST?)
-   **`-flat`:** Enable flat shading (good for combining with -celshader)
-   **`-fulldetail`:** Treat detail brushes as structural ones
-   **`-leaktest`:** Abort if a leak was found
-   **`-meta`:** Combine adjacent triangles of the same texture to surfaces (ALWAYS USE THIS)
-   **`-minsamplesize` N:** Sets minimum lightmap resolution in luxels/qu
-   **`-mi` N:** Sets the maximum number of indexes per surface
-   **`-mv` N:** Sets the maximum number of vertices of a lightmapped surface
-   **`-ne` F:** Normal epsilon for plane snapping etc.
-   **`-nocurves`:** Turn off support for patches
-   **`-nodetail`:** Leave out detail brushes
-   **`-noflares`:** Turn off support for flares
-   **`-nofog`:** Turn off support for fog volumes
-   **`-nohint`:** Turn off support for hint brushes
-   **`-nosubdivide`:** Turn off support for `q3map_tessSize` (breaks water vertex deforms)
-   **`-notjunc`:** Do not fix T-junctions (causes cracks between triangles, do not use)
-   **`-nowater`:** Turn off support for water, slime or lava (Stef, this is for you)
-   **`-np` A:** Force all surfaces to be nonplanar with a given shade angle
-   **`-onlyents`:** Only update entities in the BSP
-   **`-patchmeta`:** Turn patches into triangle meshes for display
-   **`-rename`:** Append “bsp” suffix to miscmodel shaders (needed for SoF2)
-   **`-samplesize` N:** Sets default lightmap resolution in luxels/qu
-   **`-skyfix`:** Turn sky box into six surfaces to work around ATI problems
-   **`-snap` N:** Snap brush bevel planes to the given number of units
-   **`-tempname` filename.map:** Read the MAP file from the given file name
-   **`-texrange` N:** Limit per-surface texture range to the given number of units, and subdivide surfaces like with `q3map_tessSize` if this is not met
-   **`-tmpout`:** Write the BSP file to /tmp
-   **`-verboseentities`:** Enable `-v` only for map entities, not for the world

VIS stage
---------

-   **`-vis` ... filename.map:** Switch that enters this stage
-   **`-fast`:** Very fast and crude vis calculation
-   **`-mergeportals`:** The less crude half of `-merge`, makes vis sometimes much faster but doesn’t hurt fps usually
-   **`-merge`:** Faster but still okay vis calculation
-   **`-nopassage`:** Just use PortalFlow vis (usually less fps)
-   **`-nosort`:** Do not sort the portals before calculating vis (usually slower)
-   **`-passageOnly`:** Just use PassageFlow vis (usually less fps)
-   **`-saveprt`:** Keep the PRT file after running vis (so you can run vis again)
-   **`-tmpin`:** Use /tmp folder for input
-   **`-tmpout`:** Use /tmp folder for output

LIGHT stage
-----------

-   **`-light` ... filename.map:** Switch that enters this stage
-   **`-vlight` ... filename.map:** Deprecated alias for `-light -fast` ... filename.map
-   **`-approx` N:** Vertex light approximation tolerance (never use in conjunction with deluxemapping)
-   **`-areascale` F, `-area` F:** Scaling factor for area lights (surfacelight)
-   **`-border`:** Add a red border to lightmaps for debugging
-   **`-bouncegrid`:** Also compute radiosity on the light grid
-   **`-bounceonly`:** Only compute radiosity
-   **`-bouncescale` F:** Scaling factor for radiosity
-   **`-bounce` N:** Number of bounces for radiosity
-   **`-cheapgrid`:** Use `-cheap` style lighting for radiosity
-   **`-cheap`:** Abort vertex light calculations when white is reached
-   **`-compensate` F:** Lightmap compensate (darkening factor applied after everything else)
-   **`-cpma`:** CPMA vertex lighting mode
-   **`-custinfoparms`:** Read scripts/custinfoparms.txt
-   **`-dark`:** Darken lightmap seams
-   **`-debugaxis`:** Color the lightmaps according to the lightmap axis
-   **`-debugcluster`:** Color the lightmaps according to the index of the cluster
-   **`-debugdeluxe`:** Show deluxemaps on the lightmap
-   **`-debugnormals`:** Color the lightmaps according to the direction of the surface normal
-   **`-debugorigin`:** Color the lightmaps according to the origin of the luxels
-   **`-debugsurfaces`, `-debugsurface`:** Color the lightmaps according to the index of the surface
-   **`-debugunused`:** This option does nothing
-   **`-debug`:** Mark the lightmaps according to the cluster: unmapped clusters get yellow, occluded ones get pink, flooded ones get blue overlay color, otherwise red
-   **`-deluxemode 0`:** Use modelspace deluxemaps (DarkPlaces)
-   **`-deluxemode 1`:** Use tangentspace deluxemaps
-   **`-deluxe`, `-deluxemap`:** Enable deluxemapping (light direction maps)
-   **`-dirtdebug`, `-debugdirt`:** Store the dirtmaps as lightmaps for debugging
-   **`-dirtdepth`:** Dirtmapping depth
-   **`-dirtgain`:** Dirtmapping exponent
-   **`-dirtmode 0`:** Ordered direction dirtmapping
-   **`-dirtmode 1`:** Randomized direction dirtmapping
-   **`-dirtscale`:** Dirtmapping scaling factor
-   **`-dirty`:** Enable dirtmapping
-   **`-dump`:** Dump radiosity from `-bounce` into numbered MAP file prefabs
-   **`-export`:** Export lightmaps when compile finished (like `-export` mode)
-   **`-exposure` F:** Lightmap exposure to better support overbright spots
-   **`-external`:** Force external lightmaps even if at size of internal lightmaps
-   **`-extravisnudge`:** Broken feature to nudge the luxel origin to a better vis cluster
-   **`-extrawide`:** Deprecated alias for `-super 2 -filter`
-   **`-extra`:** Deprecated alias for `-super 2`
-   **`-fastbounce`:** Use `-fast` style lighting for radiosity
-   **`-faster`:** Use a faster falloff curve for lighting; also implies `-fast`
-   **`-fastgrid`:** Use `-fast` style lighting for the light grid
-   **`-fast`:** Ignore tiny light contributions
-   **`-filter`:** Lightmap filtering
-   **`-floodlight`:** Enable floodlight (zero-effort somewhat decent lighting)
-   **`-gamma` F:** Lightmap gamma
-   **`-gridambientscale` F:** Scaling factor for the light grid ambient components only
-   **`-gridscale` F:** Scaling factor for the light grid only
-   **`-keeplights`:** Keep light entities in the BSP file after compile
-   **`-lightmapdir` directory:** Directory to store external lightmaps (default: same as map name without extension)
-   **`-lightmapsize` N:** Size of lightmaps to generate (must be a power of two)
-   **`-lomem`:** Low memory but slower lighting mode
-   **`-lowquality`:** Low quality floodlight (appears to currently break floodlight)
-   **`-minsamplesize` N:** Sets minimum lightmap resolution in luxels/qu
-   **`-nocollapse`:** Do not collapse identical lightmaps
-   **`-nodeluxe`, `-nodeluxemap`:** Disable deluxemapping
-   **`-nogrid`:** Disable grid light calculation (makes all entities fullbright)
-   **`-nolightmapsearch`:** Do not optimize lightmap packing for GPU memory usage (as doing so costs fps)
-   **`-normalmap`:** Color the lightmaps according to the direction of the surface normal (TODO is this identical to `-debugnormals`?)
-   **`-nostyle`, `-nostyles`:** Disable support for light styles
-   **`-nosurf`:** Disable tracing against surfaces (only uses BSP nodes then)
-   **`-notrace`:** Disable shadow occlusion
-   **`-novertex`:** Disable vertex lighting
-   **`-patchshadows`:** Cast shadows from patches
-   **`-pointscale` F, `-point` F:** Scaling factor for point lights (light entities)
-   **`-q3`:** Use nonlinear falloff curve by default (like Q3A)
-   **`-samplescale` F:** Scales all lightmap resolutions
-   **`-samplesize` N:** Sets default lightmap resolution in luxels/qu
-   **`-samples` N:** Adaptive supersampling quality
-   **`-scale` F:** Scaling factor for all light types
-   **`-shadeangle` A:** Angle for phong shading
-   **`-shade`:** Enable phong shading at default shade angle
-   **`-skyscale` F, `-sky` F:** Scaling factor for sky and sun light
-   **`-smooth`:** Deprecated alias for `-samples 2`
-   **`-style`, `-styles`:** Enable support for light styles
-   **`-sunonly`:** Only compute sun light
-   **`-super` N, `-supersample` N:** Ordered grid supersampling quality
-   **`-thresh` F:** Triangle subdivision threshold
-   **`-trianglecheck`:** Broken check that should ensure luxels apply to the right triangle
-   **`-trisoup`:** Convert brush faces to triangle soup
-   **`-wolf`:** Use linear falloff curve by default (like W:ET)

Analyzing BSP-like file structure
---------------------------------

-   **`-analyze` ... filename.bsp:** Switch that enters this mode
-   **`-lumpswap`:** Swap byte order in the lumps

Converting & Decompiling
------------------------

-   **`-convert` ... filename.bsp:** Switch that enters this mode
-   **`-de` number:** Distance epsilon for the conversion
-   **`-format` converter:** Select the converter (available: map, ase, or game names)
-   **`-ne` F:** Normal epsilon for the conversion
-   **`-shadersasbitmap`:** (only for ase) use the shader names as \*BITMAP key so they work as prefabs

Exporting lightmaps
-------------------

-   **`-export` filename.bsp:** Copies lightmaps from the BSP to `filename/lightmap_0000.tga` ff

Fixing AAS checksum
-------------------

-   **`-fixaas` filename.bsp:** Switch that enters this mode

Get info about BSP file
-----------------------

-   **`-info` filename.bsp:** Switch that enters this mode

Importing lightmaps
-------------------

-   **`-import` filename.bsp:** Copies lightmaps from `filename/lightmap_0000.tga` ff into the BSP

MiniMap
-------

-   **`-minimap` ... filename.bsp:** Creates a minimap of the BSP, by default writes to `../gfx/filename_mini.tga`
-   **`-black`:** Write the minimap as a black-on-transparency RGBA32 image
-   **`-boost` F:** Sets the contrast boost value (higher values make a brighter image); contrast boost is somewhat similar to gamma, but continuous even at zero
-   **`-border` F:** Sets the amount of border pixels relative to the total image size
-   **`-gray`:** Write the minimap as a white-on-black GRAY8 image
-   **`-keepaspect`:** Ensure the aspect ratio is kept (the minimap is then letterboxed to keep aspect)
-   **`-minmax` xmin ymin zmin xmax ymax zmax:** Forces specific map dimensions (note: the minimap actually uses these dimensions, scaled to the target size while keeping aspect with centering, and 1/64 of border appended to all sides)
-   **`-nokeepaspect`:** Do not ensure the aspect ratio is kept (makes it easier to use the image in your code, but looks bad together with sharpening)
-   **`-o` filename.tga:** Sets the output file name
-   **`-random` N:** Sets the randomized supersampling count (cannot be combined with `-samples`)
-   **`-samples` N:** Sets the ordered supersampling count (cannot be combined with `-random`)
-   **`-sharpen` F:** Sets the sharpening coefficient
-   **`-size` N:** Sets the width and height of the output image
-   **`-white`:** Write the minimap as a white-on-transparency RGBA32 image

Scaling
-------

-   **`-scale` S filename.bsp:** Scale uniformly
-   **`-scale` SX SY SZ filename.bsp:** Scale non-uniformly
-   **`-scale -tex` S filename.bsp:** Scale uniformly without texture lock
-   **`-scale -tex` SX SY SZ filename.bsp:** Scale non-uniformly without texture lock

