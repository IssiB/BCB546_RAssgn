---
title: "Review/IssiB_R_Assn"
author: "Ahmed_Raslan"
date: "2023-03-16"
output: html_document
---

```{r}
library(tidyverse)
library(janitor)
library(ggplot2)
library(magrittr)
```  

Error in library(janitor) : there is no package called ‘janitor’







 maize_transpose <- row_to_names(maize_transpose, 1, remove_rows_above = TRUE) %>%
   rename("SNP_ID" = "Sample_ID")
Error in row_to_names(maize_transpose, 1, remove_rows_above = TRUE) : 
  could not find function "row_to_names"


maize_transpose <- maize_transpose %>%
  rownames_to_column(var = "SNP_ID")
maize_transpose <- row_to_names(maize_transpose, 1, remove_rows_above = TRUE) %>%
  rename("SNP_ID" = "Sample_ID")


I found these two commands really good to change between row and column names:However I would suggest removing the first two rows from the data frame before running the second commands since there are not necessary for the final result.
For this, you can use this command: headsoff_transposed_maize_fang <- transposed_maize_fang[-c(1:2),]
( u can change the files names to match your files) 






For the visulaization part, I would suggest adding a title o give readers a clear idea of what the plot is about.
 You can use the ggtitle() function at the end of your command to add a title. For example:  ggtitle("Scatter Plot of SNP Positions").
 


Generally, You really did great work especially organizng your repository and explainnig your codes 