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

I got this error message after running this chunk, not quite sure what might be 
the reason, but I ran install.packages("janitor") followed by library(janitor) and it worked fine after. 




snp_position <- as.data.frame(snp_position[,c(1,3:4)]) 

I liked this command as I struggled to extract these columns by name instead of this data frame creation function. Anyways, alternatively you can use the select command to do the same thing (cut_snp_position <- select(readable_snp_position, SNP_ID, Chromosome, Position))





maize_transpose <- maize_transpose %>%
  rownames_to_column(var = "SNP_ID")
maize_transpose <- row_to_names(maize_transpose, 1, remove_rows_above = TRUE) %>%
  rename("SNP_ID" = "Sample_ID")


I found these two commands really good to change between row and column names:
However I would suggest removing the first two rows from the data frame before 
running the second commands since they are not necessary for the final result.
For this, you can use this command: headsoff_transposed_maize_fang <- transposed_maize_fang[-c(1:2),]
( u can change the files names to match your files) 


For the visulaization part, I would suggest adding a title o give readers a clear idea of what the plot is about.
 You can use the ggtitle() function at the end of your command to add a title. For example:  ggtitle("Scatter Plot of SNP Positions"). 
 



Generally, You really did great work especially organizing your repository and explaining your codes 


