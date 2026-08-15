# Blender howto

Notes on importing Inkscape/dvisvgm-produced SVGs into Blender.

## SVG import and layers

Blender's SVG importer (File → Import → Scalable Vector Graphics (.svg))
largely flattens structure — it does **not** map SVG/Inkscape layers onto
anything layer-like in Blender:

- Each SVG shape/path becomes a separate **Curve object**.
- All imported objects land in a single new **Collection**, named after
  the SVG file.
- Blender has no "layers" concept since 2.8 (replaced by Collections and
  View Layers, which are render-oriented, not organizational in the
  Inkscape-layer sense).
- Nested SVG `<g>` groups (what Inkscape layers actually are under the
  hood — see [[inkscape-howto]]) are generally **not** preserved as
  nested sub-collections; hierarchy gets flattened. Object names come
  from the SVG `id` attribute when present, not from group/layer names.
- Stacking/z-order is roughly preserved via object creation order in the
  outliner (sometimes tiny Z offsets to avoid coplanar overlap), not
  translated into real 3D depth or grouping.

## Getting layer-like organization in Blender

Two options, since the importer won't do it automatically:

1. **Manual reorganization after import** — select the relevant Curve
   objects in the outliner, press M → New Collection, per logical layer.
2. **Export each Inkscape layer as its own SVG file** (hide other layers,
   then export, or use "export selection only"), and import each file
   separately into Blender. Each import naturally lands in its own
   Collection, giving layer-like separation without manual cleanup
   afterward. This is the more scalable approach if doing this
   regularly.

Third-party Blender add-ons may offer better group/layer fidelity than
the built-in importer — worth checking if this becomes a frequent
workflow, though none has been evaluated yet for this project.
