Dpm models for Xonotic
======================

1st you need dpm compiler, get it from http://icculus.org/twilight/darkplaces/files , search for dpmodel(blahblah).zip, try to get latest one

2nd you need hl2 smd exporter for your modeling application:

- 3dsmax version 6-8 : http://www.chaosincarnate.net/cannonfodder/3dsmax.php
- Maya : check here http://developer.valvesoftware.com/wiki/Maya
- Blender : there was working smd exporter fixed by div0 at Xonotic forums. This MAY be it I’m not sure: http://ai.kurotorobert.com/xonotic/files/Blender/Exporters/hl2_smd/hl2_smd_mesh_export_div0.7z

there are 2 types of smd files

- reference smd, that contain bones and mesh and uv coords
- animation smd, that contain only animation data, each animation is in separate file

if you are using same skeleton for many models you can share animation files

dpmodel converter takes these smd files and make single dpm file that contains all model info and animations inside, lately it started to generate [.framegroups](framegroups) file too, we will need this one, it will spit lots of other strange file but you wont need them

dpmodel need configuration file, its just simple text file

it looks like that:

    # save the model as box.dpm
    model box
    # move the model this much before saving
    origin 0 0 0
    # rotate the model 0 degrees around vertical
    rotate 0
    # scale the model by this amount, 0.5 would be half size and 2.0 would be doule size
    scale 1
    # allows .framegroups file generation
    framegroups
    # load the mesh file, first reference then animation files
    scene ref.smd
    scene idle.smd fps 30
    scene pain.smd fps 30 noloop
    scene death.smd fps 10 noloop

I think that comments explained it all quite well :)

you run `dpmodel.exe configfile.txt`

and that’s all

