#R Assignment Review - Dylan Harris

Code runs well overall, only issue being that janitor was not an installed package we have used, though this was simply fixed by installing janitor.

Small thing to note for packages loaded here, there is no need to include the library commands for ggplot2 and magrittr as both of these are part of tidyverse and do not need to be loaded in again.

##Data Inspection

I appreciate that you used urls to the files needed for the project, this definently helps with reproducibility.

For cutting your snp_positions, your method is very efficient. The select command is also reasonable as it let's you specify in column names and can help avoid accidentally removing the wrong columns if you were to only go off of column positions.

For the data inspection, use of the str command was a good idea, but if you also want file size, you can use object.size to get it.

##Data Processing

```
maize_transpose <- maize_transpose %>%
  rownames_to_column(var = "SNP_ID")
```
I great use of this to bring back the matching columns needed for inner_join to work.

```
maize_increasing_chr <- function(x) {
  subset(maize_combined, maize_combined$Chromosome==x) %>%
    arrange(Position)
}
```
Very good way to do this. I was struggling around with for loops for this part and ended up giving up. This is a much better method.

```
maize_chr1_decreasing[maize_chr1_decreasing == "?/?"] <- "-/-"
```
An excellent way to change the characters here. I had no idea you could just replace characters like this. Much easier than using an actual command

Not sure its necessary to print all the chromosome files outside of R, but I could be wrong on that. If you could somehow, for loop that part or do something similar I think it would be really great. It also spits the files all over the directory, if they could be directed to their own files in the repository, that would also be ideal, thouugh I am not sure that's something you can do in R.

##Data Visualization

```
aize_pivot <- maize_combined %>% 
  pivot_longer(cols = !1:3, names_to = "ID")

maize_pivot$zygosity <- ifelse(maize_pivot$value %in% c("A/A","G/G", "T/T", "C/C"), "homozygous", 
                               ifelse(maize_pivot$value %in% c("?/?"), "unknown", "heterozygous"))
```
Good to see you have used the pivot_longer command, it does really help with formatting the data for visualization.

```
maize_pivot$zygosity <- ifelse(maize_pivot$value %in% c("A/A","G/G", "T/T", "C/C"), "homozygous", 
                               ifelse(maize_pivot$value %in% c("?/?"), "unknown", "heterozygous"))
```
A very effecient use of ifelse.	Well done!

```
maize_pivot$species <- "maize"
teosinte_pivot$species <- "teosinte"
complete<- rbind(maize_pivot, teosinte_pivot)
```
Excellent idea to assign species names to your dataframes to make facet wrapping possible. I also did not realise rbind could be used like this. Much better than remaking the dataset to be for both maize and teosinte.

```
ggplot(maize_pivot, aes(x = Chromosome, y = Position)) + 
  geom_point(color = "orange")

ggplot(teosinte_pivot, aes (x = Chromosome, y = Position)) + 
  geom_point(color = "green")

ggplot(complete, aes (x = Chromosome, y = Position)) + 
  geom_point() + 
  facet_wrap(~species)
```
Great use of facet wrapping. Sort of removes the need for the individual plots above it though, may want to consider removing those.

```
ggplot(maize_pivot) +
  geom_bar(aes(x = Chromosome, fill = zygosity), position = "fill") 

ggplot(teosinte_pivot) +
  geom_bar(aes(x = Chromosome, fill = zygosity), position = "fill")

ggplot(complete) + 
  geom_bar(aes(x = Chromosome, fill = zygosity), position = "fill") + 
  facet_wrap(~species)
```
Same as above comment.

```
ggplot(complete) + 
  geom_density(aes(x = Position, linetype = species)) + 
  facet_wrap(~value)

ggplot(complete) +
  geom_bar(aes(x = Chromosome, fill = value), position = "dodge", color = "black") + 
  facet_wrap(~species)
```
Very interesting visualizations you chose. I especially like the density plot. The bar graph is a bit hard to read due to the sheer amount of bars though.

##General Comments

Very well done project. I learned quite a bit myself from just examining your code. If there is one general thing I would recommend it would be to seperate your code into more code chunks to help delineate different aspects of the code. It makes it easier to read the outputs generated when running the chunks.