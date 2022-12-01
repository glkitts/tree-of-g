---
title: R_dataScience
tags: R, code, index, MOC
toc: true
---

# R Data Science Tips and Tricks

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



## working with images

### pdfs - imagemagick - rr

```{r}
model.plt <- magick::image_read_pdf(path = '/home/rreggiar/figures/aale_model_cropped.pdf')

wrap_elements(full = magick::image_ggplot(model.plt))

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