Player Model Spec
=================

TODO stuff about exporting

TODO stuff about animations

Size
----

Dimension x, y:

                     |
     +---------------|---------------+  +16
     |               |               |
     |               |               |
     |               |               |
     |      +--------|--------+      |  +9
     |      |HEAD    |        |      |
     |      |SHOT    |        |      |
     |      |        |        |      |
     |      |        |origin  |      |
    -----------------+-----------------  0 
     |      |        |        |      |
     |      |        |        |      |
     |      |        |        |      |
     |      |        |        |      |
     |      +--------|--------+      |  -9
     |               |               |
     |               |               |
     |               |               |
     +---------------|---------------+ -16
                     |
    -16    -9        0       +9     +16

Dimension x/y, z:

                     |
     +------+--------+--------+------+  +45
     |      |HEAD    |        |      |
     |      |SHOT    |        |      |
     |      |        |        |      |
     |      |        |view    |      |
     |      |        *ofs     |      |  +35
     |      |        |        |      |
     |      +--------|--------+      |  +32
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |origin         |
    -----------------+-----------------   0
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     +---------------|---------------+ -24
                     |
    -16    -9        0       +9     +16

Dimension x/y, z when crouched:

                     |
     +------+--------+--------+------+  +25
     |      |HEAD    |        |      |
     |      |SHOT    |        |      |
     |      |        |        |      |
     |      |        |view    |      |
     |      |        *ofs     |      |  +15
     |      |        |        |      |
     |      +--------|--------+      |  +12
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |origin         |
    -----------------+-----------------   0
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     |               |               |
     +---------------|---------------+ -24
                     |
    -16    -9        0       +9     +16
