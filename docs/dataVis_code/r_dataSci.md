---
title: R_dataScience
tags: R, code, index, MOC
toc: true
---

# R Data Science Tips and Tricks

```toc
max_depth: 2
```
---

# Subpages

- [[rTips_figures_graphs|Tips and guides for figure making with a focus on scientific publication]]
- [[code_folder_organization|Optimal folder organization for lab data analyses]]
- [[r_markdown|Rmd and Quarto tricks]]
- [[color_palettes]]

---

# Topics

## General

### naming and formatting of lab data for consistent syntax 

I wish my naming to use a similar nomenclature between experiments/projects/etc. so that my downstream parsing with R can be as straightforward as possible. I will try to use standardized nomenclature moving forward. Specifics of that can be listed here. 

- experimental datasets
	- file name: exp_date
		- date format: YYMMDD
		- experiment format = two letter abbreviations
		- i.e. gc_220204
			- growth curves on 02/04/2022

#### experiment specifics

- CIs
	- excel file input: ci_date name
	- needed sheets: input and output
	- input label in both sheets, connects two upon join.
	- extra sheets optional, preferrably avoided
	- input file can host metadata - since generally one 'row' of input (ON culture) per strain, 


## importing data 

### multiple excel files in a folder:

- can use list.files for all .xlsx in a directory
- then readxl with excel_sheets for multi-sheet files


## data parsing

### filter out rows so that only counts > 0 in at least two of the columns remain

used to remove rows from proteomics data 

```{r}
d %>% 
  filter(rowSums(across(.cols = starts_with("cts_O"), .fns = ~ . > 0)) >= 2) %>%
  filter(rowSums(across(.cols = starts_with("cts_M"), .fns = ~ . > 0)) >= 2)
  ```

## ggplot

### How to arrange NAs first for plotting using dplyr

[Use the is.na logical for sorting](https://stackoverflow.com/questions/43343590/how-to-sort-putting-nas-first-in-dplyr) 

```r
tbl %>%
   arrange(!is.na(val), val)
# A tibble: 10 × 2
#      id       val
#   <chr>     <dbl>
#1      f        NA
#2      i 0.1346666
#3      c 0.2861395
#4      g 0.5190959
#5      e 0.6417455
#6      j 0.6569923
#7      h 0.7365883
#8      d 0.8304476
#9      a 0.9148060
#10     b 0.9370754
```


## patchwork

### figure alignment hacking

- when wrap_elements(full = ) doesn't allow alignment, try adding plot margin (pre-wrapping using npc units for just one axis to be increased - i.e. use 0.02 npc on bottom margin and test until aligned)

## working with images

### pdfs - imagemagick - rr

```{r}
model.plt <- magick::image_read_pdf(path = '/home/rreggiar/figures/aale_model_cropped.pdf')

wrap_elements(full = magick::image_ggplot(model.plt))

```


## rstatix

```{r}
plotdata.ci_phospho <- plotdata.ci_all %>% 
  filter(condition == "in_vivo") %>% 
  filter((as.character(date) == "2022-10-26" & 
            strain == "∆rvvA RvvB::D57E") | 
           (as.character(date) == "2023-04-20" & 
              strain %in% c(
                "WT",
                "∆rvvA RvvB::D57A",
                "∆rvvA RvvB::D57E")))


statdata <- plotdata.ci_phospho %>%
  rstatix::tukey_hsd(CI ~ label_md) %>%
  rstatix::add_significance(
    cutpoints = stat_cut,
    symbols = stat_symbols
  ) %>%
  rstatix::adjust_pvalue() %>%
  rstatix::add_y_position(
    fun = "max", 
    ref.group = "WT", 
    y.trans = log10
  )

d.statlist <- d.statlist %>%
  append(list(CI_in_vivo_phosphomimics = statdata))

  
p.ci.phospho <- plotdata.ci_phospho %>%
  # p.ci.mouse <- d.ci.all %>%
  filter(condition == "in_vivo") %>%
  ggplot(aes(
    x = label_md,
    y = CI
  )) +
  pt.ci() + 
  ggpubr::stat_pvalue_manual(
    data = statdata,
    y.position = 0.38,
    label = "p.adj.signif",
    x = "group2", 
    hide.ns = T,
    remove.bracket = T,
    # step.group.by = "phospho_set",
    # tip.length = 0.01
      )

```

