# Text Clipping

PDF supports advanced text render modes as described in clause 9.3.6 "Text rendering mode" including several modes which add gylph outlines to the current clip path. In order to ensure correct rendering behaviour with these text rendering modes, it is important to know the precise times at which the clip path is to be updated: 

> The behaviour of the clipping modes requires further explanation. Glyph outlines shall begin accumulating if a `BT` operator is executed while the text rendering mode is set to a clipping mode or if it is set to a clipping mode within a text object. Glyphs shall accumulate until the text object is ended by an `ET` operator; the text rendering mode shall not be changed back to a nonclipping mode before that point.

and:

> At the end of the text object identified by the `ET` operator the accumulated glyph outlines, if any, shall be combined into a single path, treating the individual outlines as subpaths of that path and applying the non-zero winding number rule (see 8.5.3.3.2, "Non-zero winding number rule"). The current clipping path in the graphics state shall be set to the intersection of this path with the previous clipping path. As is the case for path objects, this clipping shall occur after all filling and stroking operations for the text object have occurred. It remains in effect until a previous clipping path is restored by an invocation of the `Q` operator.

These requirements clearly indicate that clip path updating ONLY occurs at the end of the text object when the `ET` operator is encountered - it does NOT occur when the `Tr` is changed mid-way through a text object.

[TextClippingModeChanges.pdf](TextClippingModeChanges.pdf)

This hand-coded text centric PDF test file uses various PDF clipping text rendering modes to test whether the glyph outlines are correctly added at the end of each text object (i.e., the `ET` operator). Text is painted over the top of other text using various clipping text rendering modes before being used as a clip on a coloured rectangle (e.g., for stroked and clipped text, `5 Tr`, the painted rectangle will then appear in the hollow glyph outlines).
