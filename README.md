SVG2DXF
=======

`svg2dxf` is yet another converter from SVG to DXF file formats.

Though the script should fairly generic, it has been created with Inkscape and
OpenSCAD in mind.

## Usage

The `svg2dxf` script is called with 2 parameters, the input file and the output
file:

    svg2dxf input.svg output.dxf

## Requirements

`svg2dxf` uses:

- Inkscape
- pstoedit

They are widely available in standard repositories of any decent GNU/Linux
distribution.

## Tips

### Preparing the SVG file with Inkscape

The script is meant to convert SVG files created with Inkscape to DXF files
that can be imported in OpenSCAD.

The script cannot do anything required to smoothly import your image in
OpenSCAD. That's why you must give it a hand by preparing your file in Inkscape:

- use only one layer
- use only black color
- ungroup everything (Edit → Select all ctrl+A, Object → Ungroup shift+ctrl+G
  until there is no more group)
- convert straight lines et Bézier curves to paths (Path → Stroke to path
  ctrl+alt+c)
- convert circles, ellipses, rectangles and other geometric forms to paths (Path
  → Object to path shift+ctrl+C)
- remove flats
- do a union of all objects (Edit → Select all ctrl+A, Path → Union ctrl++)

You should have only one object with black background and no stroke remaining.

Following theses tipes should avoid you to have a DXF file that is unsuable by
OpenSCAD.

### Using the DXF file in OpenSCAD

The generated DXF should have only one layer named "0".

The following code can be used to import the DXF file in OpenSCAD:

    translate([-40,-60,0])
         linear_extrude(height = 30, convexity = 5)
             import(file = "zigazou.dxf", layer = "0");

## Why another SVG to DXF converter?

- it tests requirements before doing anything
- it uses no temporary file at all (everything is done in a pipe)
- I like to rewrite things
