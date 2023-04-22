---
tags: ["guides_protocols", "learning", "digital_garden"]
---

# Sequence alignment tools and tips

```toc
```
---


- What is % identity threshold for proteins?
	- Can model / consider similar at >20%

## Finding similar genes / proteins

### Based on sequence similarity

---

#### BLAST

| BLAST type | Query sequence                     | Database                           | Alignment  | Use                                                              |
| ---------- | ---------------------------------- | ---------------------------------- | ---------- | ---------------------------------------------------------------- |
| blastn     | nucleotide                         | nucleotide                         | nucleotide | sequence identity, useful for all taxa categories                |
| blastx     | nucleotide (translated to protein) | protein                            | protein    | Identify encoded proteins, detection of novel viruses            |
| blastp     | protein                            | protein                            | protein    | sequence ID and similarity search                                |
| tblastx    | nucleotide (translated to protein) | nucleotide (translated to protein  | protein    | ID nucleotide sequences with coding regions similar to the query |
| tblastn    | protein                            | nucleotide (translated to protein) | protein    | ID database sequences encoding proteins similar to the query     |


---

### Based on predicted structural similarity

- [Phyre2](http://www.sbg.bio.ic.ac.uk/~phyre2/html/page.cgi?id=index)
- [i-TASSER](https://zhanggroup.org/I-TASSER/)
- AlphaFold structures





