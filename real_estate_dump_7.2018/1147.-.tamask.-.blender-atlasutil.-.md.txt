blender-atlasutil
=================

Texture atlas packer utilities for Blender 2.6, with no external
dependencies, to aid with atlas generation for game assets.

Installation
------------

Drop the `atlasutil` python module into Blender's `scripts/modules`
path.

Defining Libraries
------------------

`atlasutil` has a function for collecting objects, merging their
textures into atlases and updating their UVs and saving them into a
library blendfile.

The contents of the library blendfile to be generated is defined in a
python script, a lot like regular Python `setup.py` scripts.  Here is
an example, let's call it `fruit.py`:

    from atlasutil import library

    sources = (
        '/path/to/apples.blend',
        '/path/to/oranges.blend',
    )

    library.make(
        blendfile='/path/to/output/fruits.blend',
        sources=(
            '/path/to/apples.blend',
            '/path/to/oranges.blend',
        )
        atlases=(
            # atlas format string followed by
            # groups to pull from the sources
            (
                'apples@512x512',  
                'gala',
                'fuji',
                'granny_smith',
                'mc_intosh',
                'golden_delicious',
            ),
            (
                'oranges@512x512', # atlas format string
                'valencia',
                'blood',
                'navel',
            )
        )
    
Atlases are defined as a list of strings, where the first string
is the atlas format:

    [name]@[width]x[height]

Optionally you can provide a margin and trim value for the packer,
which are both `0` by default:
    
    [name]@[width]x[height]:[margin]:[trim]

The remaining items in the atlas list are the group names to consider
as part of the atlas, as well as their constituent objects and
textures.  You can also tune the size of textures for a any of the
listed groups like this:

    [group]@[maxsize]

This will constrain any textures used by that group to that size or
smaller.  This is useful if you want to fine-tune how much real estate
each group's textures take up in the atlas.  For example:

    (
        'oranges@512x512', # atlas format string
        'valencia@64',
        'blood@128',
        'navel@64',
    )

If a texture is used by multiple groups, the highest `maxsize` defined
will be used.

Currently `atlasutil` doesn't automatically sequence atlases into
multiple textures if not all textures can fit. Each atlas texture
needs to be explicitly defined in the configuration script.

Generating Libraries
--------------------

You can build the library blendfile with configuration Python scripts
described above.  For example:
    
    blender -b -P fruit.py
    
This is what happens when making a library blendfile:

* All groups are appended to the library blendfile

* Atlases collect their constituent groups/objects and their
  dependent textures.

* Textures are packed according to the parameters set in the
  config script

* Texture atlases are rendered using Blender itself, and output
  into a `textures` directory alongside the library blendfile

* The UVs and textures of objects are updated to use the atlas
  textures generated.

If the textures collected for an atlas cannot fit into the specified
atlas, a `PackOverflow` error will be thrown.

Texture Channels
----------------
    
`atlasutil`'s library generation makes some decisions about how atlas
textures are generated.  Currently, `atlasutil` interprets a number of
'channels' from a material's textures: `color`, `specular`, `normal`
and `emit`.  A separate atlas image is generated for each channel so
that the object's UVs remain effective for these properties.

These mappings should probably be configurable at some point, but
their not at the moment (see
`atlasutil.library.LibraryAtlas.collect_images()` for details).

Generic Packing Utilities
-------------------------

You can use the packer directly:

    from atlasutil import packer

    packer.pack(
        objects=(
            {name: 'a', 'width': 128, 'height': 32},
            {name: 'b', 'width': 12, 'height': 80},
            ...
        ),
        width=1024, height=1024,
        margin=1, trim=0
    )

You can pass `pack` an arbitrary list of objects, they just need to
have either `width` and `height` attributes or dictionary items which
define their dimensions during packing.

`margin` adds the specified margin around objects as they are packed,
whereas `trim` shrinks the size of the resulting rectangles by the
amount specified.

Generic Atlas Rendering Utilities
---------------------------------

You can also use the renderer directly (rendering is done with Blender
itself).  Rendering is done this way so there are no dependencies on
external image compositing libraries:

    from atlasutil import renderer

    renderer.render(
        filename='output.png',
        width=1024, height=1024,
        quads=(
            # (texture, (x, y, width, height))
            ('path/to/texture_a.png', (0, 0, 128, 128)),
            ('path/to/texture_b.png', (129, 0, 128, 128)),
            ...
        )
    )

Currently `render` always outputs as `PNG` format.
