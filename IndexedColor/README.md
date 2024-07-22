# Indexed Colour spaces with out-of-range indices

The PDF specification has always defined the behaviour for indexed colour spaces when indexed with out-of-range indices: last paragraph of PDF 2.0 (ISO 32000-2) clause 8.6.6.3 "Indexed colour spaces" states:

> The index value should be an integer in the range 0 to _hival_. If the value is a real number, it shall be rounded to the nearest integer (0.5 values shall be rounded up); if it is outside the range 0 to _hival_, it shall be adjusted to the nearest value within that range.

PDF 2.0 only clarified that the rounding rule was to always _round up_ when at 0.5 to ensure consistent behaviour between implementations, otherwise this requirement has remained unchanged for many years.

This effectively means that all out-of-range indices will be snapped to either the 0 index (for values below 0) or the _hival_ index colour for valules above the _hival_ value in the colour space object.

[IndexedCS_negative_and_high.pdf](IndexedCS_negative_and_high.pdf)

This simple hand-coded text centric test PDF contains a single PDF Indexed colour space with 8 values (indices 0 to 7 inclusive). There are 2 rows of colour patches - the bottom row are the correct reference patches and the top row are the test patches. The 1st (left most) and last 2 (right most) patches on the top row represent out-of-range indices (the 2nd last patch has index 6.5 and gets round up, while the last patch is index 17 and needs to be snapped back to _hival_). When indexed with values below 0, the 0-th indexed colour needs to be used and when indexed with values above 7, the 7th indexed colour needs to be used, thus both rows should match exactly. 
