


### Password protected html output

You must first knit your Rmd file to html. Once that has occured, from R console or elsewhere, you can load in the already knitted html file and create an encrypted version. 

- Works well in tests so far
- Adds a bit of file size to output, as expected

```{r}
library(pagecryptr)
if(interactive()){
 file <- "fileName.html"
 pagecryptr(file, "password", out_file = "~/Desktop/encrypted-file.html")
}
```

