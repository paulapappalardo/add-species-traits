# Add species traits

This repo includes R functions to add species traits based on species names and higher taxonomy. For now, I am releasing the first version with a single function to add plankton groups. More functions to come!

## Add Plankton group

The first version of this function was published in Pappalardo et al, 2021:

Paula Pappalardo, Allen G Collins, Katrina M Pagenkopp Lohan, Kate M Hanson, Sarit B Truskey, William Jaeckle, Cheryl Lewis Ames, Jessica A Goodheart, Stephanie L Bush, Leann M Biancani, Ellen E Strong, Michael Vecchione, M G Harasewych, Karen Reed, Chan Lin, Elise C Hartil, Jessica Whelpley, Jamie Blumberg, Kenan Matterson, Niamh E Redmond, Allison Becker, Michael J Boyle & Karen J Osborn. The role of taxonomic expertise in interpretation of metabarcoding studies, ICES Journal of Marine Science, Volume 78, Issue 9, November 2021, Pages 3397–3410, https://doi.org/10.1093/icesjms/fsab082

The goal was to use __broad taxonomic categories__ to separate taxa found in plankton samples into __holoplankton and meroplankton__. Based on our experience detecting some organisms that do not quite fit this classification, we also added a few additional categories:

* Holoplankton: organisms that live permanently within the water column (e.g., most copepods, comb jellies).
* Meroplankton:  planktonic life-history stages of benthic organisms that live temporarily in the water column (e.g. eggs, larvae, and adults in the case of medusozoan cnidarians). For example, larvae of decapod crabs.
* Benthic: This category includes benthic organisms without a planktonic larva. For example, Naineris dendritica, a benthic polychaete that has aplanktonic development (Grantham et al., 2004). This category can also include benthic/sedentary organisms that have a benthic larval stage (e.g., some harpacticoid copepods).
* Holo/Mero: when the classification is uncertain (e.g., for some families of polychaetes where both plankton groups have been reported).

We also highlighted taxa that are parasites when possible. For example, for the family Pyramidellidae the classification is "Meroplankton - parasite of invertebrates". Or for some copepods, the classification is "Holoplankton - fish parasites". Users can remove these flags by retaining only the text before the dashes.

The taxonomic focus is __metazoans__. The development of the function began with advice from Karen Osborn and Allen Collins of the NMNH Invertebrate Zoology Department, National Museum of Natural History, Smithsonian Institution, while working on the Pappalardo et al. (2021) publication. Since then, Paula Pappalardo has been updating this function with further research, often searching specific species or smaller taxonomic groups and adding taxonomic levels as in NCBI or WoRMS taxonomy. There are comments in the function that point to particular websites where information on larval development was found. Often, all members of a phylum belong to the same plankton type (e.g., all Sipuncula were meroplankton). But for many groups (e.g., Annelida, Arthropoda), we provide taxonomic filters that involve taxonomic assignments below the level of phylum (i.e, Class, Order, Family). After working on additional projects, new classifications have been added at the genus and species levels to the original function. Paula has also utilized her life history database, InvertTraits (unpublished - forthcoming), to enhance the classification of plankton groups. A publication and release for InvertTraits is in the making. You can check Paula's website for updates: https://paulapappalardo.weebly.com/. There are comments within the function indicating when the information was taken from InvertTraits. 

There are differences in higher taxonomy classification across different taxonomic databases. For example, as of October 2025, the GBIF taxonomic backbone includes barnacles within the class Maxillopoda, while WoRMS includes them in the class Thecostraca. The code accommodates these differences, ensuring the function works correctly regardless of the higher taxonomy used. That said, taxonomy is constantly evolving, and not all existing cases may have been noted. If you find other cases that should be included, please open an issue.  

If you have suggestions for improvement, please open an issue. Paula will regularly update this function and release new versions when significant changes accumulate.

CITATION: Please cite this repo and the original Pappalardo et al., 2021 publication.

DEPENDENCIES: The function requires the R packages [dplyr](https://dplyr.tidyverse.org/) and [taxize](https://docs.ropensci.org/taxize/articles/taxize.html).

USAGE: this is an R function taking a dataframe or tibble as the argument. The dataframe needs to include columns for phylum, class, order, family, genus and species. Based on this, the function returns the same dataframe with an additional column, called "plankton_group", appended. How to use:

```r

edited_df <- addPlanktonGroup(your_df)

edited_df <- your_df %>% addPlanktonGroup() # if using dplyr and pipes
```


