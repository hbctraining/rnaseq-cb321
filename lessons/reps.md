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

- **Splice-isoform differential expression:**

  - For known isoforms, suggested to have a depth of at least 30 million reads per sample and paired-end reads.

  - For novel isoforms should have more depth (> 60 million reads per sample).

  - Choose biological replicates over paired/deeper sequencing.
  
- **Other types of RNA analyses (intron retention, small RNA-Seq, etc.):** 
  
  - Different recommendations depending on the analysis.
  
  - Almost always more biological replicates are better!
  
