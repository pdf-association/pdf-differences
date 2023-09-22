# PDF Differences

![LinkedIn](https://img.shields.io/static/v1?style=social&label=LinkedIn&logo=linkedin&message=PDF-Association)
&nbsp;&nbsp;&nbsp;
![Twitter Follow](https://img.shields.io/twitter/follow/PDFAssociation?style=social)
&nbsp;&nbsp;&nbsp;
![YouTube Channel Subscribers](https://img.shields.io/youtube/channel/subscribers/UCJL_M0VH2lm65gvGVarUTKQ?style=social)

This is a _private_ (PDF Association member-only) repository for responsible reporting of commonly-seen PDF issues to PDF Association members prior to any public disclosure. It is intended to allow PDF Association members to test and address any potential implementation issues within a fixed but reasonable timeframe of 60 days before wider public discussion and dissemination. The PDF files in this repository are targeted test files highlighting specific issues seen across multiple widely-used implementations. Implementations at fault will **not** be named or identified - it is a member responsibility to assess their own technology.

The issues identified in this repository are **not** security related - they impact portability and interoperability; PDF's "prime directive"!

Detailed documentation for each test case is provided as MarkDown files and in an associated article on https://www.pdfa.org. Access to this documentation will be restricted to PDF Association members for 60 days (the "responsible reporting period") before being made public, as communicated via email to PDF Association members.

Once 60 days have passed PDF files in this repository are _moved_ to the public repository `pdf-differences` with the associated article on https://www.pdfa.org updated accordingly. By _moving_ the PDF test files, development teams can monitor this members-only repository knowing that there is a 60 day window to successfully process all files contained therein. This approach avoids any potential divergence of test files between this members-only and the public `pdf-differences` repositories.

The issues demonstrated by PDF files in this repository may be discussed in any [PDF Association TWG](https://pdfa.org/community/), as TWGs, unlike LWGs, are member-only forums. Please do not post any information publicly until the 60 day responsible reporting period has passed.

# The PDF test files

* PDF files are as minimal (short) as possible and well-commented internally.

* PDF files are pure text except for the 2nd line comment with 4 binary bytes. This is so they may be easily viewed in text editors and development environments used by software developers. 

* PDF files have valid conventional cross-reference tables with ample whitespace and line-breaks to further enable easy reading.

* PDF header versions are 1.7. These files do not cover new features or change to features introduced in PDF 2.0 unless explicitly noted otherwise.

* PDF files avoid excessive on-page descriptive text as this makes files larger and more internally complex, obscuring the purpose of allowing developers to quickly and easily understand each test case.

* To further ensure rapidity and ease of comprehension, these PDF files purposely do **not** use many "best practices" such as metadata, embedded fonts, device independent color, etc., and they avoid other large data or complex features that inhibit direct inspection in a text editor (such as Linearization, XMP, cross-reference streams, object streams, compacted syntax, etc) unless necessary to the test case.

* Screenshots used in the ReadMe files have been purposely resized to 600 pix wide after capture. Screenshots should **not** be compared at a pixel level to determine correctness (the image processing was a small attempt at trying to stop this)!!

* Correct renderings are always the _last_ image in the MarkDown, encouraging readers to read everything for a full understanding of the correct appearance.

---

PDF files are copyright by the PDF Association and distributed under a [Creative Common Attribution 4.0 International (CC BY 4.0) license](https://creativecommons.org/licenses/by/4.0/). Any source code in this repository is licensed under [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.html).
