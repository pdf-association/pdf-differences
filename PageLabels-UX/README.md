# Page Labels

ISO 32000-2:2020, clause 12.4.2 defines Page Labels as a means of optimizing the page navigation experience for users via support for flexible page identifiers.

End-user page navigation to arbitary pages is often enabled by direct user entry into a page number/label text widget. Optimal support allows users to enter alphanumeric and Unicode to match against a descriptive page label rather than always assume every documents uses Arabic page numbering starting from 1.

PDF Page Labels can support the use of any Unicode-based counting system, even if not directly supported by the **S** entry. For example, Traditional Chinese characters can be supported by defining a **P** entry for _each page_ with the appropriate Unicode string and not having **S** or **St** entries. See the last 3 pages in [PageLabels.tex]. 
