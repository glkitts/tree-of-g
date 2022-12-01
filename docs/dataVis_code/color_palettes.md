---
tags: [dataSci]
---


- [Mega list of color palettes in R sorted by type and color-blind friendly etc.](https://github.com/EmilHvitfeldt/r-color-palettes/blob/master/type-sorted-palettes.md#qualitative-color-palettes)
- [Coloring for colorblindness](https://davidmathlogic.com/colorblind/#%23D81B60-%231E88E5-%23FFC107-%23004D40)

## Types of color palettes

- Qualitative/categorical - This is for groups/strains/categorical variables
	- unique colors that can be differentiated easily i.e. strains 
- Sequential
	- Increasing gradient style palette, usually an increasing gradient of one color or transitioning through multiple
	- Optimally is perceptually uniform and also displays correctly in grayscale - i.e. [viridis color palettes](https://cran.r-project.org/web/packages/viridis/vignettes/intro-to-viridis.html) are great for these purposes
- Divergent
	- Classic heatmap style palette to represent decreasing and increasing changes with different colors (i.e. red is decreasing and blue is increasing with white at the center)
	- Divergent palettes generally have a central point where something like white is present so that areas with little change (i.e. close to 0 fold-change for genes) will be shown in a more neutral color such as white. 

