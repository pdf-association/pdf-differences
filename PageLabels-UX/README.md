# PDF-UX: Page Labels

The files in this folder are described in the article "[PDF-UX: Page Labels](https://pdfa.org/pdf-ux-page-labels/)" on the PDF Association website.

ISO 32000-2:2020, clause 12.4.2 defines Page Labels as a means of optimizing the page navigation experience for users via support for flexible page identifiers, including Roman numerals, Arabic numbers and alphabetic page identifiers.

![PDF forensic tool view of page labels](https://pdfa.org/wp-content/uploads/2024/08/RUPS.png)

End-user page navigation to arbitary pages is often enabled by direct user entry into a page number/label text widget. Optimal support allows users to enter alphanumeric and Unicode to match against a descriptive page label rather than always assume every documents uses Arabic page numbering starting from 1.

![PDF Page Label dialog](https://pdfa.org/wp-content/uploads/2024/08/pl2.png)

PDF Page Labels can support the use of any Unicode-based counting system, even if not directly supported by the **S** entry. For example, Traditional Chinese characters can be supported by defining a **P** entry for _each page_ with the appropriate Unicode string and not having **S** or **St** entries. See the last 3 pages in "(PageLabels.tex)[PageLabels.tex]" which can be can be loaded into the online [Overleaf](https://www.overleaf.com/) system. 

The simple Microsoft Word ([PageLabels.docx](PageLabels.docx)) and Apple Pages ([PageLabels.pages](PageLabels.pages)) test documents  utilize the built-in capabilities of these word processing formats for different kinds of page numbering across different sections for testing export to PDF capabilities.
