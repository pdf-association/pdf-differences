# PDF Versions

With an increased awareness of file format correctness, reporting the PDF version of a file seems like a simple task. However, [past analysis](https://pdfa.org/pdf-versions/) shows that PDF versions are both unreliable as indication of PDF features, and unreliably reported by some PDF software.

ISO 32000-2:2020, 7.5.2 "File header" describes the process that software must use:

1. the PDF file header has a version e.g. `%PDF-1.4`.

2. the Document Catalog may have a **Version** key (_which is a PDF name, not a number!_) which can upgrade (increase) the version present in the file header.

3. any incremental update can also upgrade version, by provided a new Document Catalog with an upgraded (increased) **Version** entry.
    - Due to other file trailer requirements in incremental updates, if the Document Catalog needs to be modified for an unrelated change, then any existing **Version** entry needs to be duplicated (and thus remain the same PDF version).

[PDF Errata #399](https://github.com/pdf-association/pdf-issues/issues/399) [clarified](https://pdf-issues.pdfa.org/32000-2-2020/clause07.html#H7.5.6) that Document Catalog **Version** entries can only increase (or be the same) as the PDF version of the previous file revision. They cannot "downgrade" a PDF version.

## Test files

The correct reported version for all test PDFs is PDF 1.6.

### [PDF-version1.pdf](PDF-version1.pdf)

1. the header is `%PDF-1.4`.

2. the Document Catalog of the original document has a **Version** entry of PDF 1.5 (i.e. `/1.5` when written as a PDF name object).

3. there is a single incremental update that replaces the Document Catalog using a PDF object with an updated generation number (i.e., `1 1 obj`).  This new Document Catalog sets the **Version** to PDF 1.6 (i.e., `/1.6` when written as a PDF name object).

### [PDF-version2.pdf](PDF-version2.pdf)

1. the header is `%PDF-1.4`.

2. the Document Catalog of the original document has a **Version** entry of PDF 1.5 (i.e. `/1.5` when written as a PDF name object).

3. there is a single incremental update that replaces the Document Catalog object of the original file with a new PDF object (object 5, i.e., `5 0 obj`).  This new Document Catalog sets the **Version** to PDF 1.6 (i.e. `/1.6` when written as a PDF name object).

### [PDF-version3.pdf](PDF-version3.pdf)

The same as [PDF-version2.pdf](PDF-version2.pdf), but additionally uses a PDF 2.0 specific feature (**UseBlackPtComp** in a graphics state parameter dictionary) in the original PDF for software that does runtime comparisons of PDF version and PDF feature sets. For example, software based on the [Arlington PDF Model](https://github.com/pdf-association/arlington-pdf-model/) should report an inconsistency of a PDF 2.0 feature being present in a PDF 1.6 file.
