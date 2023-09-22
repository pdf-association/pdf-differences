# Inline image abbreviated and full key names

This example is copied from [PDF Association's SafeDocs GitHub repo](https://github.com/pdf-association/safedocs/tree/main/Inline%20Image%20Abbreviations). It was originally publicized by [this article](https://www.pdfa.org/safedocs-unearths-pdf-inline-image-issue/).

The follow inline image key name abbreviations are defined in "Table 91 - Entries in an inline image object" in ISO 32000-2:2020:

| Full Name | Abbreviation |
| --------- | :----------: |
| `BitsPerComponent` | `BPC` |
| `ColorSpace`       |  `CS` |
| `Decode`           |  `D` |
| `DecodeParms`      |  `DP` |
| `Filter`           |  `F` |
| `Height`           |  `H` |
| `ImageMask`        |  `IM` |
| `Interpolate`      |  `I` (uppercase i) |
| `Length` (_PDF 2.0_) |  `L` |
| `Width`            |  `W` |


No PDF specification or standard, including [ISO 32000-2:2020](https://www.iso.org/standard/75839.html) provides guidance on how PDF processors should behave if both a full key name **and** the matching abbreviated key name are present in a single inline image dictionary.

This question was raised as [GitHub pdf-issue #3](https://github.com/pdf-association/pdf-issues/issues/3) and resolved by the [addition of the following statement to clause 8.9.7](https://pdf-issues.pdfa.org/32000-2-2020/clause08.html#H8.9.7) in ISO 32000-2:2020:

> "In the situation where both an abbreviated key name and the corresponding full key name from Table 91 are present, the abbreviated key name shall take precedence."

The inline image syntax constructs used in this PDF test file use the following rules:
* they are all valid according to ISO 32000-2:2020
* they are otherwise self-consistent for both the all-full and all-abbreviated key interpretations
* beneath each image (in Z-order) is a green coloured rectangle to assist in identifying any rendering issues. If you see a green rectangle, that's a **FAIL!**
* key values for keys not being tested are valid and correct for the image data provided
* the image is natively 20 x 10 pixels, 8 bit RGB, and always less than 4KB in the PDF file (meeting inline image requirements). It is also therefore heavily up-scaled.

![The test image](image.png)

This test PDF contains 8 individual test cases for various sets of full and abbreviated keys, as it should not be assumed that PDF processors might do "all full keys" or "all abbreviated keys". Each test case:

1. Baseline. Only full key names are used - _all PDF processors should support this!_
2. Baseline. Only abbreviated key names are used - _all PDF processors should support this!_
3. The `/Width` and `/Height` keys have different (incorrect) values compared to `/W` and `/H`.
4. The `/Filter` key is being tested with an incorrect value for the inline image data (whereas `/F` is correct). This also likely means the inline image pixel data will confuse the PDF parser and it may not be able to process further test cases.
5. The `/ColorSpace` key uses an extreme `CalRGB` colorspace which will make the image appear different in failing processors, whereas `/CS` uses `/RGB` (DeviceRGB)
6. The `/Decode` array is the linear inverse of `/D` and thus the image will display differently in failing processors.
7. The `/Interpolate` key is true and, for those processors that support image interpolation, the image will display differently in failing processors.
8. The `/DecodeParms` key is missing key information which will make the image display differently in failing processors.

## Correct appearance
Correct output is the same image in all 8 locations:

![Correct page appearance](InlineAbbreviations-correct.png)

The PDF test file is a pure text file with comments. By commenting out a few lines in each test case, the image can be visualised as to what failing might look like.

In some cases, PDF processors may struggle to recover from content stream errors and display all 8 test cases. In these cases, it is recommended to comment out the triggering inline image key(s) of the last visible test case and see if the PDF processor will then processor more of the PDF.

## Notes on how this PDF was manually constructed

* the file `image.raw` is a hand-coded (in a hex editor!) raw 20 x 10 pixmap, with 24 bits per RGB pixel (8 bits per component). It can be opened and visualized directly by tools such as [IrfanView](https://www.irfanview.com/) which can then also be used to "Save As" JPEG (`DCTDecode`) or JPEG 2000 (`JPXDecode`).

* the following simple Linux shell commands can be used to convert any data to various stream formats suitable for direct inclusion into PDF. These commands can also be cascaded to create filter chains:

```bash
# To ASCIIHex:
od -A n -v -t x1 < data.raw | sed -e 's/ *//g' > data.hex
# then add a final ">" (EOD marker) when inserting into the PDF

# From ASCIIHex (can include the final ">" EOD marker):
xxd -r -p < data.hex > data.raw

# To FLATE:
zlib-flate -compress < data.raw > data.flate

# From FLATE:
zlib-flate -uncompress < data.flate > data.raw
```

# Sample Output from PDF viewers
Here is the output from some failing viewers:

![Viewer1](Viewer1.png)
![Viewer2](Viewer2.png)
![Viewer3](Viewer3.png)
![Viewer4](Viewer4.png)


If test 4 is nullified (i.e. it is converted to a valid inline image by commenting out this line `% /Filter [/A85]` by changing the first `SPACE` to a `%`), then this showed more failures:

![Viewer1b](Viewer1b.png)
![Viewer3b](Viewer3b.png)
![Viewer4b](Viewer4b.png)

# Related Publications

- "[_Room for Disagreement_](https://galois.com/blog/2021/11/room-for-disagreement/)"; Bill Harris, Nichole Schimanski, Peter Wyatt; November 2, 2021.
- "[_SafeDocs unearths PDF inline image issue_](https://www.pdfa.org/safedocs-unearths-pdf-inline-image-issue/)"; Peter Wyatt; November 8, 2021.
- "[_SafeDocs - towards a more secure future_](https://youtu.be/2DZwaIOYGjA?t=652)" (YouTube, starting at 10'52); Peter Wyatt; PDF Days 2021 virtual event.
