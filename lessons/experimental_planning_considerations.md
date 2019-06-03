# Experimental design considerations

Understanding the steps in the experimental process of RNA extraction and preparation of RNA-Seq libraries is helpful for designing an RNA-Seq experiment, but there are special considerations that should be highlighted that can greatly affect the quality of a differential expression analysis. 

These important considerations include:

1. Number and type of **replicates**
2. Avoiding **confounding**
3. Addressing **batch effects**

We will go over each of these considerations in detail, discussing best practice and optimal design.

## Replicates

Experimental replicates can be performed as **technical replicates** or **biological replicates**. 

<img src="../img/replicates.png" width="400">

*Image credit: [Klaus B., EMBO J (2015) **34**: 2727-2730](https://dx.doi.org/10.15252%2Fembj.201592958)*

- **Technical replicates:** use the same biological sample to repeat the technical or experimental steps in order to accurately measure technical variation and remove it during analysis. 

- **Biological replicates** use different biological samples of the same condition to measure the biological variation between samples. 

In the days of microarrays, technical replicates were considered a necessity; however, with the current RNA-Seq technologies, technical variation is much lower than biological variation and **technical replicates are unneccessary**.

In contrast, **biological replicates are absolutely essential**. For differential expression analysis, the more biological replicates, the better the estimates of biological variation and the more precise our estimates of the mean expression levels. This leads to more accurate modeling of our data and identification of more differentially expressed genes.

<img src="../img/de_replicates_img.png" width="500">

*Image credit: [Liu, Y., et al., Bioinformatics (2014) **30**(3): 301–304](https://doi.org/10.1093/bioinformatics/btt688)*

As the figure above illustrates, **biological replicates are of greater importance than sequencing depth**. The figure shows the relationship between sequencing depth and number of replicates on the number of differentially expressed genes identified [[1](https://academic.oup.com/bioinformatics/article/30/3/301/228651/RNA-seq-differential-expression-studies-more)]. Note that an **increase in the number of replicates tends to return more DE genes than increasing the sequencing depth**. Therefore, generally more replicates are better than higher sequencing depth, with the caveat that higher depth is required for detection of lowly expressed DE genes and for performing isoform-level differential expression. 

Replicates are almost always preferred to greater sequencing depth for bulk RNA-Seq. However, guidelines depend on the experiment performed and the desired analysis. Below we list some general guidelines for replicates and sequencing depth to help with experimental planning:

- **General gene-level differential expression:**

  - [ENCODE guidelines](https://www.encodeproject.org/documents/cede0cbe-d324-4ce7-ace4-f0c3eddf5972/@@download/attachment/ENCODE%20Best%20Practices%20for%20RNA_v2.pdf) suggest 30 million SE reads per sample (stranded).
  
  - 15 million reads per sample is often sufficient, if there are at least 4 replicates. 

  - More replicates >> More sequencing depth

- **Gene-level differential expression with detection of lowly-expressed genes:**
  
  - Sequence deeper with at least 30-60 million reads depending on level of expression (start with 30 million with a good number of replicates). 
  
  - Similarly benefits from replicates more than sequencing depth.

> *Additional applications:*
>
> - **Splice-isoform differential expression:**
> 
>   - For known isoforms, suggested to have a depth of at least 30 million reads per sample and paired-end reads.
> 
>   - For novel isoforms should have more depth (> 60 million reads per sample).
> 
>   - Choose biological replicates over paired/deeper sequencing.
>   
> - **Other types of RNA analyses (intron retention, small RNA-Seq, etc.):** 
>   
>   - Different recommendations depending on the analysis.
>   
>   - Almost always more biological replicates are better!
  
## Confounding
  
A confounded RNA-Seq experiment is one where you **cannot distinguish the separate effects of two different sources of variation** in the data. 

For example, we know that sex has large effects on gene expression, and if all of our *control* mice were female and all of the *treatment* mice were male, then our treatment effect would be confounded by sex. **We could not differentiate the effect of treatment from the effect of sex.**

<img src="../img/confounded_design.png" width="500">  

**To AVOID confounding:**

- Ensure animals in each condition are all the **same sex, age, litter, and batch**, if possible.

- If not possible, then ensure to split the animals equally between conditions

  <img src="../img/non_confounded_design.png" width="400">

## Batch effects

Batch effects are a significant issue for RNA-seq analyses, since you can see significant differences in expression due solely to batch.

<img src="../img/batch_effect_pca.png" width="600">

*Image credit: [Hicks SC, et al., bioRxiv (2015)](https://www.biorxiv.org/content/early/2015/08/25/025528)*

### How to know whether you have batches?

- Were all RNA isolations performed on the same day?

- Were all library preparations performed on the same day?

- Did the same person perform the RNA isolation/library preparation for all samples?

- Did you use the same reagents/kits for all samples?

- Did you perform the RNA isolation/library preparation in the same location?

If *any* of the answers is **‘No’**, then you have batches.

### Best practices regarding batches:

- Design the experiment from start to finish to **avoid batches**, if possible. If unsure of what can bring in a batch effect, talk with a biostats consultant before starting experiment.

- If unable to avoid batches:

  - **Do NOT confound** your experiment by batch:

    <img src="../img/confounded_batch.png" width="300">
    
    *Image credit: [Hicks SC, et al., bioRxiv (2015)](https://www.biorxiv.org/content/early/2015/08/25/025528)*
  
  - **DO** split replicates of the different sample groups across batches. The more replicates the better (definitely 3 or more).
  
    <img src="../img/batch_effect.png" width="300">

    *Image credit: [Hicks SC, et al., bioRxiv (2015)](https://www.biorxiv.org/content/early/2015/08/25/025528)*
    
  - **DO** include batch information in your **experimental metadata**. During the analysis, we can regress out the variation due to batch so it doesn’t affect our results if we have that information.

    <img src="../img/metadata_batch.png" width="300">
    
 ***
